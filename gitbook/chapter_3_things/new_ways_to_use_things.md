## New Ways to Use Things

Inform’s model of how things exist (and can be used) in the world is very simple. Sometimes you’ll want the player to be able to do something new or unexpected with a thing. In this section we’ll borrow some ideas from Chapter 4, “Actions,” and show you how to allow new kinds of actions with the objects in your game. For details on how Check, Carry Out, Report, and Instead rules work, consult Chapter 4. The main purpose of the section you’re now reading is to show how to do interesting things with the new objects you’ve created.

This section was inspired by an old post on rec.arts.int-fiction, which I spotted while poking around in the ifwiki (http://www.ifwiki.org/). The list of new actions suggested by Jan Thorsby in that post was short but suggestive: holding an object close to or against another object, holding an object up in the air, threatening an NPC with an object or tipping a bookshelf forward so that the thing on the top shelf will fall down. I’ll leave you to explore the process of threatening an NPC for yourself. The other three actions are illustrated below.

The number of new things you might want players to be able to do is probably infinite. Some of them will turn out to be easy to set up; others may be surprisingly tricky for you to implement. The key, in each case, is to think logically and try to handle all of the things a player might do. You’ll also need to consider all of the states that your objects might get themselves into. For example, you may know that you only want your new tipping action to apply to one object in the game — but once players know that the TIP command works, they’ll surely try it on anything and everything. So you need to write a check rule for your new action that will handle any and all of players’ attempts with a sensible-sounding refusal message. You may also want to write an in-game clue to suggest that tipping something might be a good action to try. For instance, in a description of an object: “It looks as if it might tip over in a strong breeze.”

### Holding Something Up in the Air

The player might very reasonably want to hold an object up in the air so as to make it visible to an NPC who is far away. (If the NPC is in the same room, a standard command of the form SHOW JEWEL TO PRINCESS should do the job.) You might want to hold up a white sheet, for instance, if you’re marooned on an island and trying to attract the attention of a passing ship. Below is a simple example game that implements this action. Notice the long list of input grammar that is allowed. You’d probably want to add even more grammar lines to this list if you’re using this action in a game.

The key point in this example is that the sheet has to be held aloft for three consecutive turns on the beach in order to signal the passing ship. If the player drops the sheet or walks west into the jungle, the sheet is no longer aloft, and the count drops back to zero. Taking care of details like these will add realism to your game.

The details are taken care of by the after dropping something and after going rules, and by the new property called aloft. Every object in the game can be aloft or not — but most of them won’t be, so this new property will only be useful in a few cases.

Why make aloft a general property of all things, when you’re only going to be using it for one object? Because it reduces the chance of bugs, and makes your code easier to maintain and expand. If you should later be writing a different section and decide that the player needs to hold a torch aloft, you don’t have to go back and revise anything, because the torch already has that property.

```inform7
A thing can be aloft. A thing is usually not aloft. A thing has a number called the aloft-count. The aloft-count of a thing is usually 0.

The Beach is a room. The player carries a white sheet.

Elevating is an action applying to one thing. Understand "hold [something preferably held] up", "hold up [something preferably held]", "wave [something preferably held]", "elevate [something preferably held]", "hold [something preferably held] aloft", "hold [something preferably held] in the air", "hold [something preferably held] in air", and "hold [something preferably held] up in the air" as elevating.

Check elevating:
        if the noun is not held:
                say "You'll need to pick up [the noun] first.";
                rule fails.

Carry out elevating:
        now the noun is aloft;
        say "You hold [the noun] high in the air."

After dropping something:
        now the noun is not aloft;
        now the aloft-count of the noun is 0;
        continue the action.

After going:
        repeat with item running through things carried by the player:
                now item is not aloft;
                now the aloft-count of item is 0;
        continue the action.

The Jungle is west of the Beach.

Every turn:

if the white sheet is aloft and the location is the Beach:

increase the aloft-count of the white sheet by 1;

if aloft-count of the white sheet is 4:

end the story saying "A passing ship spots your signal, and steers in toward shore. You're saved!"

### Tipping Something {#tipping-something}

Placing an object out of reach — on a high shelf or down at the bottom of a well, for instance — is a standard puzzle in IF (see Chapter 6, “Puzzles”). Some high shelves are fixed to the wall, but some might be the top shelf in a heavy bookcase that can’t be moved, but can be rocked or tipped. In the example below, note that the pushing action (which is part of Inform’s standard library) has been remapped to the new rocking action.

```inform7
The Living Room is a room. "The only furniture here is a tall bookshelf."

The bookshelf is a scenery supporter in the Living Room. "It's so tall you can't possibly reach the top shelf -- and oddly enough, there's only one shelf, the top one." Understand "top", "shelf", and "bookcase" as the bookshelf.

The Ming vase is on the bookshelf. The description is "A priceless vase!"

Instead of putting anything on the bookshelf:
        say "You can't reach the top shelf."

Instead of doing something other than examining when the noun is not nothing and the noun is on the bookshelf:
        say "You can't reach [the noun], as the shelf is too high."

Rocking is an action applying to one thing and requiring light. Understand "tip [something]", "rock [something]", "shake [something]", "tip [something] forward", and "rock [something] forward" as rocking.

Check rocking:
        say "There's no need to agitate [the noun]."

Instead of rocking the bookshelf:
        if the Ming vase is on the bookshelf:
                now the player carries the Ming vase;
                say "You give the shelf a good shake ... and the vase teeters forward, reaches the edge, and plummets! Fortunately, you're able to catch it just before it hits the floor.";
        otherwise:
                say "There's nothing else up there."

Instead of pushing the bookshelf:
        try rocking the bookshelf.

### Holding Something Against Something Else {#holding-something-against-something-else}

This example creates a new action, holding it against. This action has two Report rules. The thing you need to know is that when your game is being compiled, Inform assembles all of the rules, including those in the standard library, those in any extensions you have included, and any you have written yourself, into rulebooks. _Both_ of our new rules will end up in the report holding it against rulebook — but Inform has some very specific criteria (let’s not call them rules, as that would be confusing) about how to do this. It puts more specific rules near the top of the rulebook, and more general rules later in the rulebook.

As a result, the Report holding the stethoscope against the wall rule will be earlier in the “report holding it against” rulebook. When this rulebook is being consulted (after the player has used the command HOLD STETHOSCOPE AGAINST WALL, for instance), Inform will consult the rulebook _until one of the rules makes a decision_. Then it will stop. For this reason, we’ll end the specific rule with the line “rule succeeds.” This will prevent the more general rule from being applied.

```inform7
The Cell is a room. "A dank, rat-infested cell. Faint murmurings can be heard from the other side of the wall."

A stethoscope is here. The stethoscope is wearable. Understand "scope" as the stethoscope.

Report wearing the stethoscope:
        say "You insert the ear-pieces into your ears.";
        rule succeeds.

The wall is scenery in the Cell. The description is "Solid cement blocks."

Holding it against is an action applying to two things. Understand "hold [something] against [something]", "press [something] against [something]", and "apply [something] to [something]" as holding it against.

Check holding it against:
        if the player does not enclose the noun:
                say "You'll need to be holding [the noun] in order to do that.";
                rule fails.

Report holding it against:
        say "You press [the noun] against [the second noun] for a moment, but nothing seems to have been accomplished by this."

Report holding the stethoscope against the wall:
        if the player wears the stethoscope:
        say "You press the stethoscope against the wall. [one of]After a moment you hear a man's voice as distinctly as if he were in the cell with you: 'Good thing he doesn't know I hid the key in the light fixture!'[or]In the next room, two men are discussing horse racing. Since you already know where the key is hidden, there's probably no need to keep listening.[stopping]";
        rule succeeds.

Notice the non-default message that’s printed out when the player wears the stethoscope. Also notice the use of “[one of] … [or] … [stopping]” to insure that the conversation about the hidden key is printed out only once.

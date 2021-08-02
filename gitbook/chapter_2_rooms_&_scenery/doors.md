## Doors

In the real world, most indoor rooms are separated by doors. In Inform, a door is a special type of object because it’s in two rooms at once and connects the two. In this section but we’ll look at a couple of ways to improve on the default doors.

To create a door, create the rooms on both sides of the door first, but _don’t_ connect the rooms by mentioning directions. If you mention the directional connection between the rooms, Inform won’t let you create a door between them. After creating the rooms, create the door, and tell Inform about its directions with respect to the two rooms:

```inform7
The Entry Hall is a room.
The Billiard Room is a room.
The oak door is a door. The oak door is north of the Billiard Room and south of the Entry Hall.
```

We can’t just name the oak door using the word “door”: We have to add that extra sentence telling Inform that the door is a door. The following will compile, but it’s an error:

```inform7
The Entry Hall is a room.
The Billiard Room is a room.
The oak door is north of the Billiard Room and south of the Entry Hall. [Error!]
```

If we write it this way, Inform will think “oak door” is the name of a room. It will create a third room called oak door, which will lie between the other two rooms. You might think that Inform should understand that calling something a door makes it a door, but that could conceivably cause unexpected problems. What if you were creating rooms named after science fiction novels, and wanted a room called The Door Into Summer? To avoid this type of confusion, the compiler needs to be cautious so you’ll have to write the extra sentence.

If you include the code shown above (the first three lines, not the second three) in your game, you’ll notice that the door itself will be mentioned by the game’s output along with any other objects in the room. In other words, a door is not scenery unless we make it scenery.

Inform’s doors start out closed unless the author says otherwise, but will be automatically opened to allow the player to travel from place to place:

```
>s
(first opening the oak door)

Billiard Room
You can see an oak door here.
```

If you find “(first opening the oak door)” distracting, one solution is not to make the room connections doors at all. When you need to mention a connection between rooms in your room description, just call it a “doorway.” Most players won’t mind if you sacrifice a bit of realism in order to make the game work more smoothly. There’s usually not much need for doors unless they’re part of a puzzle, or unless they’re so obviously part of the scene that omitting them would be unrealistic.

You can use the door kind in Inform to make other room-connecting objects, such as gates, ladders, and bridges. A ladder or bridge probably wouldn’t be openable: You’d want it to be permanently open. The reason to make it a door is so that it will be visible in both of the rooms that it connects. For instance:

```inform7
The wooden bridge is a scenery door. The wooden bridge is south of the Meadow and north of the Forest Path. The wooden bridge is open and not openable. The description is "It's a handsome old bridge. Curiously, there's no creek running beneath it."
```inform7

It’s handy that Inform understands the command CROSS BRIDGE. If you consult the Index/Actions page in the IDE, you’ll discover that CROSS is a synonym for ENTER, so you don’t need to code it yourself. But if you create a ladder using the door kind, you’ll need to write an Instead rule to handle CLIMB LADDER:

```inform7
Instead of climbing the rickety ladder:
        try entering the rickety ladder.
```

Inform doors are unusual in a couple of ways. First, a door can’t be moved. If you write a rule like this:

```inform7
After throwing the brass lever:
        now the weird door is in the Cellar.
```

...the compiler will compile it, but you’ll get a run-time error when you play the game. The error message will explain that doors can’t be moved.

Second, unlike most other objects in your Inform code, a door object is in two rooms at once. This makes sense, but it can lead to a problem. If you put an ornate silver door knocker on one side of the front door, the knocker will be visible on the inside of the door, even when the door is closed! A simple solution in this case is to use the extension Deluxe Doors by Emily Short. This extension allows you to create “half-doors,” each of which represents only one side of the door, and to keep them in sync, so that when the player opens or closes one of the half-doors, the other opens or closes as well.

### Locked Doors

![](../assets/graphics26.jpg)

A locked door is a slightly different matter. Personally, I feel that a locked door and hidden key don’t make for a very entertaining puzzle. Hundreds of games have included locked doors, and if there’s a doormat or a potted plant anywhere nearby, players will instantly know to LOOK UNDER MAT and SEARCH POT. There’s just not much fun in it anymore. I have played with this cliché in a couple of ways. In one game I included both a locked door that can never be opened because there isn’t a key, and a locked door to which another character spontaneously gives the player a key without even being asked for it. Doors that can only be unlocked from one side (after you find a secret entrance to the room) are slightly more interesting.

Here’s how to create a locked door in Inform, and how to make it friendly for the player. If the player carries the correct key, the door will be unlocked

```inform7
The oak door is north of the Billiard Room and south of the Entry Hall. The oak door is a door. The oak door is scenery. The oak door is lockable and locked. The brass key unlocks the oak door.

Before going through the oak door:
        if the oak door is closed and the oak door is locked:
                if the player carries the brass key:
                        say "(first unlocking the oak door with the brass key, then opening the door)[paragraph break]";
                        now the oak door is unlocked;
                        now the oak door is open.
The player carries the brass key.
```

Several new elements are introduced above. First, I’ve written a Before rule. Later in this chapter you’ll see examples of Instead and After rules. To learn how these rules work, and how to employ them in your code, see [here](.../chapter_4_actions/action_processing.md#action-processing). Next, and more to the point in this particular example, if something can be opened and closed, we’re allowed to make it lockable. Lockable is a property of certain kinds of objects: Doors and containers can be made lockable, but nothing else. (Technically, this is not quite true. We can also make a new kind of object — perhaps a detonator — and allow objects of that kind to be lockable and locked.) Next, if something is lockable, at the beginning of the game is can be either locked or unlocked. During the game, the player who has the right key can unlock it — or your code can do so in response to some action by the player. For instance, a door with an old-fashioned bar might be locked and unlocked using the commands BAR DOOR and UNBAR DOOR. Such a door might not have a key at all.

You could write code so that a lockable door became not lockable, but this would only become useful if there was a way within the game to break the lock. Most often, a thing that is lockable will remain lockable (and unlockable, obviously) throughout the game.

If you read **p. 3.13**, “Locks and Keys,” in _Writing with Inform_, you’ll learn three different ways to tell Inform that a certain key can be used to unlock a lockable thing. The sentence used above, “The brass key unlocks the oak door,” seems the simplest.

In Inform, a lockable thing can have only one key. This is not usually a big problem. If you need to, though, you can write an Instead rule that will allow a second key to do the unlocking job. Here’s a rather silly example. Let’s suppose we’ve already told Inform that the tiny key unlocks the gold amulet, but we also want to be able to use the banana as a key:

```inform7
Instead of unlocking the gold amulet with the banana:
        if the player does not carry the banana:
                say "You don't seem to be holding the banana.";
        otherwise if the amulet is not locked:
                say "The gold amulet doesn't seem to be locked.";
        otherwise:
                now the amulet is not locked;
                say "You unlock the gold amulet with the banana."
```

If you create the oak door as shown on the previous page, the oak door will automatically be unlocked and then opened if the player carries the key. The only downside of this code is that it assumes the player _knows_ the brass key unlocks the oak door. If you want to force the player to discover that fact, you’ll have to work out a way to track what the player knows. Keeping track of the player’s (or the player character’s) knowledge is not difficult to manage, but the details may differ from one game to the next. The extension Epistemology by Eric Eve is designed to make it easy to track the player’s knowledge.

### Secret Doors

More interesting in a game than a locked door is a secret door — something that doesn’t appear to be a door at all until its presence is revealed. Secret Doors by Andrew Owen is a simple extension that allows you to create secret doors. This extension is available on the Inform 7 website, but there are two problems with it. First, the word “when” is repeated in two of its rules. This is easily fixed by editing. The other is that it relies on an outmoded method for printing error messages. To learn how to fix this, see Appendix B.

If you include this extension and then create a secret door, the door will pretend not to exist until something happens in the game that causes it to be revealed. For instance, if the door is disguised as oak wall paneling, this would work:

```inform7
Include Secret Doors by Andrew Owen.

The Billiard Room is a room. "Hand-rubbed oak paneling adds a warm glow above the broad green felt surface of the billiard table."

The Small Windowless Room is a room. "It smells dusty in here, as if the secret door hasn't been opened in ages."

The oak door is north of the Billiard Room and south of the Small Windowless Room. The oak door is a secret door.

The oak wall paneling is scenery in the Billiard Room. The description is "Richly carved oak paneling covers the north wall[if the oak door is open]. One of the panels has been opened; it’s actually a door[otherwise if the oak door is revealed]. One of the panels has an unusually wide seam around it[end if]." Understand "carved" and "panel" as the paneling.

After examining the oak wall paneling for the first time:
        now the oak door is revealed;
        say "One of the panels has an unusually wide seam around it. On closer inspection, the panel proves to be a door!"
```

This produces exactly the type of interaction we’d expect of a secret door:

```
>n
You can't go that way.

>open door
You can't see any such thing.

>x paneling
Richly carved oak paneling covers the north wall.

One of the panels has an unusually wide seam around it. On closer inspection, the panel proves to be a door!

>open door
You open the oak door.

>n

Small Windowless Room
It smells dusty in here, as if the secret door hasn't been opened in ages.
```

### Dangerous Doors

When I was teaching some younger students the basics of IF, one them asked how to create a door that would slam shut behind the player. I thought this might make an interesting puzzle, so I wrote it up. The example below shows how to use an After rule to affect what happens when the player travels from one room to another:

```inform7
The Corridor is a room. "The corridor stretches east and west from here. A massive stone door stands invitingly open to the north."

The Dank Cell is a room. "This cramped chamber smells of mold, and other things that are a lot less pleasant than mold. You can hear rats scurrying behind the walls. A massive stone door to the south is the only visible exit ... using the term 'exit' loosely, as the door [one of]has just slammed shut with a sound suggestive of finality and doom[or]is firmly shut[stopping]."

The massive stone door is a door. The massive stone door is scenery. The massive stone door is north of the Corridor and south of the Dank Cell. The description is "It's quite an imposing-looking stone door." The massive stone door is open, lockable, and locked.

Instead of closing the massive stone door:
        if the massive stone door is open:
                say "...but it looks so inviting! Why not just step through it and see what's on the other side?";
        otherwise:
                say "It seems already to have closed itself without your lifting a finger."

After going north from the Corridor:
        now the massive stone door is closed;
        say "As you step through the stone door, it swings shut with a terrible loud BOOM!";
        continue the action.
```

You’ll notice that the massive stone door is initially open — but also initially locked. Inform is happy to create a locked door that’s open. As soon as the door is closed, its locked condition will keep it from being opened again.

To learn more about the syntax in the room description, which includes “[one of]” and “[stopping]”, see “Text Insertions” [here](../chapter_9_phrasing_&_punctuation/text_insertions.md#text-insertions).

If this door were used in a real game, there would of course be some sort of hidden exit from the Dank Cell. Devising a hidden exit from a cell that seems not to have any exits … well, let’s just say I’ve seen a few authors try it, and some of their attempts were more convincing than others. The idea that there might be a trapdoor under the straw on the floor doesn’t quite work for me: Why would any sensible jailer ever build a cell with a trapdoor in the floor? Giving the player a tool with which to loosen the bars on the window might make a better puzzle.

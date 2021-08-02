## Code Optimization

In the 1970s, when the very first interactive fiction games were written, computers were (by today’s standards) incredibly slow, and had almost no memory. As a result, games — and every other type of software — had to be written very efficiently. If the software had to do a lot of churning, the user might issue a command and then have to wait ten or twenty seconds for the computer’s response. Or all afternoon. Issue a command, then go out for coffee, or come back tomorrow morning to find out if your program did what you expected it to. This was annoying, to say the least.

Today’s computers are incredibly fast, and have gigantic memory capacities. So there’s no longer any need to think about optimizing your game code.

At least, that was true ten years ago, when Inform 7 was first designed. But since then, a couple of developments in the world of personal computing have changed the picture somewhat.

First, text games are now being played on hand-held devices such as cell phones. These gadgets have less memory than a desktop Mac or PC, and their processors are slower too. Until next-generation hand-helds get faster and boast more memory, optimizing your game so that it will run smoothly on this growing family of devices will be important.

But there’s a bigger issue. Two new interpreters, Parchment (for .z5 and .z8 games) and Quixe (for Glulx games) have been released that run directly in Web browsers. This is a terrific development, as it opens up the potential audience for IF to millions of people who would be unlikely to download a separate interpreter program. Other browser-based terps are also appearing. What they have in common is that they’re written in a language called Javascript. You don’t need to know a blessed thing about Javascript in order to see your games running on one of these interpreters — but you need to understand that Javascript can be slow. Five years from now that bottleneck may have gone away, and IF authors will be free to write free-wheeling, inefficient games. Until then, you may want to think about utilizing a few programming techniques that will optimize your Inform games.

For the following discussion, I’m relying on information from Ron Newcomb, Andrew Plotkin, and others. They know a lot more about Inform, and about programming in general, than I do. (Plotkin created Quixe, in fact.)

### Instead of Instead

As noted in the box on _Efficiency Tips_ [here](../chapter_4_actions/action_processing.md#action-processing), Inform’s mechanism for processing the player’s input by means of rulebooks called Before, Instead, and After is inefficient. This is because there’s only one of each of these rulebooks. On the other hand, each action (such as EXAMINE, TAKE, and DROP) has its own Check, Carry Out, and Report rulebooks. What this means is that each time the player enters a command, the game will consult _all_ of the Before, Instead, and After rules that you’ve written to see if any of them applies. In a large game, that could be hundreds of rules.

In many cases, you can easily replace Instead rules with Check and Carry Out rules and After rules with Carry Out and/or Report rules. Let’s start with a simple Check rule:

```inform7
The player carries a rotten banana. The banana is edible.

Check eating the banana:
        say "Ewwww!" instead.

[Instead of eating the banana:
        say "Ewwww!"] [This produces the same result, but it's less efficient.]
```

The main difference between the two rules is that the Check rule has to have the word “instead” tacked onto the end. If you forget to do this (and it’s easy to forget), Inform will consult the Check rule and then go on to run the Carry Out and Report rules for the action. The word “instead” causes the rule to succeed, which is a technical way of saying that nothing else will happen.

In exactly the same way, we can replace an After rule with a Report rule, like this:

```inform7
[After eating the banana:
        say "After chowing down on the banana, you feel a little ill."] [Not efficient.]

Report eating the banana:
        say "After chowing down on the banana, you feel a little ill.";
        rule succeeds.
```

Again, we have to tack on a little extra syntax (“rule succeeds”) to shut off Inform’s default Report rule for the eating action — but if you’re concerned about efficiency, this is a small price to pay.

Rewriting a Before rule as a Check or Carry Out rule is trickier, if only because Before rules are intended for situations that are a little tricky. I tend to use Before rules mostly in constructions like this:

```inform7
Before doing anything other than examining to the sky, say "The sky is too far away." instead.
```

This type of construction (“anything other than...”) can’t be used in Check or Carry Out rules, simply because each action has its own set of rulebooks.

### Every Turn Rules

In every turn, every Every Turn rule in your game will be consulted to see whether it’s relevant. As your Every Turn rules proliferate, the game will become less efficient. Fortunately, most of your Every Turn rules will probably be targeted at specific circumstances, such as when a certain scene is active or when the player is in a certain room. If you group all of the Every Turn rules that apply to a given situation as if-tests within a single rule, you’ll gain efficiency. For instance:

```inform7
Every turn when in the Glue Factory:
        if the security guard is in the Factory:
                say "The guard belches loudly.";
        if Esmerelda is in the Factory:
                say "Esmerelda sighs winsomely.";
        if the blast furnace is heated:
                say "Heat radiates from the blast furnace.";
        [...and so on...]
```

When the player is in the Glue Factory, the fact that the rules are grouped will change nothing — but whenever the player is _not_ in the Glue Factory, only one Every Turn rule will be consulted to see whether it applies, rather than several of them.

### Other Ways to Streamline Your Code

Occasionally, the “after reading a command” activity will prove very useful. But it runs each time the player types the Return key, so putting a lot of if-tests in it will slow the game down. I’ve run into one or two aspiring authors who thought it would be cool to basically reinvent the parser by putting a bunch of stuff in the “after reading a command” activity. To do this, they tried to write lots and lots of code to figure out whether the player’s command included specific words. That’s the parser’s job. If you can use an offstage object, a backdrop, or an invisible part of the player, any of which can be given vocabulary words, to direct the parser to the result you’re trying to create, that will be more efficient — and also friendlier to the player and less likely to include bugs.

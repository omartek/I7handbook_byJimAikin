## Every Turn Rules {#every-turn-rules}

We’ve already seen a couple of examples of Every Turn rules. As you can guess from the name of the rule, an Every Turn rule is consulted every turn to see whether it would like to do anything. This rule is consulted as the _last_ step in the process that starts when the player types a command. The output of an Every Turn rule will normally appear at the bottom of a block of text in the game, after the description of whatever happens as a result of the player’s latest command.

An Every Turn rule can print out some text, or it can do something more complicated. Printing out some text is a nice way to add atmosphere to your game, but a message that prints every turn will quickly become annoying. Here’s an Every Turn rule that adds atmosphere to a forest setting in a slightly more interesting way. Sometimes it chooses a random text to print, and sometimes it does nothing:

```inform7
Every turn:
        if a random chance of 1 in 3 succeeds:
                say "[one of]A dragonfly darts past you.[or]You hear a frog croaking.[or]A bird chirps in the bushes.[or]The breeze rustles the leaves.[at random]".
```

But even with a bit of randomness, this type of Every Turn rule will get boring before very long. A better solution is to write an Every Turn rule that only runs when a certain scene is happening, or when the player is in a certain region. If we have defined the Forest Area as a region, we could rewrite the rule above like this:

```inform7
Every turn when the player is in the Forest Area:
```

If we’ve created a scene called Forest Explorations, we could do it this way:

```inform7
Every turn during Forest Explorations:
```

In fact, if you’re concerned about writing efficient code so that your game won’t be sluggish when played in the current generation of Web browsers (and this is something to be concerned about), qualifying your Every Turn rules in this way, so that they’re only consulted by the game when specific scenes are active, is a good idea.

We can also write an Every Turn rule that will produce some narrative or background text at specific points within a scene. Here, the phrase “exactly three turns” will insure that the output text is produced only once (unless the scene is recurring, in which case it will be produced once per recurrence):

```inform7
Every turn:
        if Saucer Menace has been happening for exactly three turns:
                say "You hear an odd glorping noise somewhere nearby.";
        otherwise if Saucer Menace has been happening for exactly five turns:
                say "Was that a tentacle you saw slithering out of sight?"
```

An Every Turn rule can also wait quietly in the background, checking for a certain set of conditions, and then do something when the conditions are met. Here’s a simple game that shows how the idea might work:

```inform7
The Throne Room is a room. "The king's golden throne stands here."

The golden throne is an enterable scenery supporter in the Throne Room. The description is "A magnificent golden throne."

The jewelled sceptre is here. The sparkling crown is here. The crown is wearable.

Every turn:
        if the player wears the sparkling crown and the player carries the jewelled sceptre and the player is on the golden throne:
                say "You're the king!!!";
                end the story saying “Congratulations!”

Every turn, this rule checks to see whether the player has done all three things that are needed to win: the player has to be carrying the sceptre and wearing the crown while sitting on the throne. You could get the same results using After rules for three different actions (after taking the sceptre, after wearing the crown, and entering the throne), and test in each of the After rules for whether the other two conditions were satisfied — but using an Every Turn rule is less likely to lead to a bug, because you can test all three conditions in one place. And if you need to edit the code for some reason, you only need to edit it in one place; you don’t need to hunt for every spot in the code where that condition is being checked.

Here’s another way to get the same result:

```inform7
Every turn when the player is on the golden throne:
        if the player wears the sparkling crown and the player carries the jewelled sceptre:
                say "You're the king!!!";
                end the story saying “Congratulations!”
```

As this example shows, an Every Turn rule can include a test in its first line. If we’re writing a game in which the player needs to eat periodically, we might do something like this:

```inform7
A person can be hungry or not hungry. A person is usually not hungry.
The player has a number called hunger-level. The hunger-level of the player is 0.
Every turn when the player is hungry:
        increase the hunger-level of the player by 1;
        say "[one of]Your stomach is rumbling.[or]You're becoming quite hungry.[or]You're very hungry. You need to find food soon.[or]You're practically starving![stopping]";
        if the hunger-level of the player is 7:
                end the story saying "You have starved to death!"
```

Switching the player to hungry would happen elsewhere in the code. In this example we’ve added something new — a counter (hunger-level) that keeps track of how long the player has been hungry, and ends the game after a set number of turns. When the player eats food, your code would both switch the player to not hungry and reset the hunger-level of the player to 0.

# Chapter 7: Winning &amp; Losing {#chapter-7-winning-losing}

![](../assets/graphics14.png)

Inform has no built-in concept of “winning” or “losing” — it’s up to you to define how your game will end. To end the game, put the phrase “end the story” in a rule somewhere — perhaps like this:

```inform7
The Forest is a room. "Tall trees stand on all sides."

The gold crown is in the Forest. The description is "The crown is studded with sparkling jewels!"

After taking the crown:
        end the story saying “You have won!”

The player carries a cyanide pill. The cyanide pill is edible.

After eating the cyanide pill:
        end the story saying “Alas, you have died.”
```

An After rule is a good place to end the game, because it gives Inform a chance to make sure the action actually took place before ending the game.

If you don’t add your own text to the “end the story” command, Inform will simply print out “\*\*\* The End \*\*\*". It’s usually a good idea to write a line immediately before the “end the story” line, in order to describe what the player has done to end the game before officially ending it. We might revise our code like this:

```inform7
After taking the crown:
        say "At last! You've found the gold crown you've been seeking!";
        end the story saying “You have won!”

After eating the cyanide pill:
        say "Moments after ingesting the pill, you begin to feel very, very ill.";
        end the story saying “Alas, you have died.”
```

This is fine as far as it goes, but sometimes the end of a game calls for something less drastic than the death of the player character. Depending on the story, maybe the game should detect that the player is giving up too soon. In that case, you could do this:

```inform7
Instead of going north in the Forest:
        say "As you wander back down the mountainside toward town, you feel a keen and lingering sense of regret.";
        end the story saying "You have missed the point entirely!"
```

After the phrase “end the story saying”, you can give whatever message you like. This will appear, surrounded by the rows of asterisks, when the game ends.

Oddly enough, “end the story” is a phrase that _must_ include the word “the”. More often than not, Inform strips out “the” when compiling, but here it’s required.

On **p. 9.4** of _Writing with Inform,_ “When play ends,” a distinction is made between “end the story” and “end the story finally.” I haven’t been able to figure out exactly what the difference is. I suggest just using “end the story” without worrying about “finally.”

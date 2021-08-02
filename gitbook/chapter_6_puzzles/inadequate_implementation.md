## Inadequate Implementation

This isn’t really a type of puzzle, except in the technical sense: It’s a design flaw ― and a serious one. In an inadequate implementation puzzle (which can be of almost any type), the player lacks necessary information because the author has neglected to include it, either in the output text or in the software code. The “puzzle” boils down to making random guesses or reading the author’s mind, which is pretty much the same thing.

The most common subtype of the inadequate implementation puzzle is called a guess-the-verb puzzle. You (the player) can see exactly what you need to do to solve the puzzle, but the author has failed to write code that handles any of the obvious and appropriate commands that you try. Very few things are more infuriating for an IF player than trying ‘stab guard with sword’, ‘cut guard with sword’, ‘kill guard’, ‘attack guard with sword’, and so on, being met in each case with a blank refusal by the game, only to find that the correct syntax is ‘swing sword’ while you’re in the room with the guard.

Another subtype is the inadequately described room or object. Describing the manner in which a complex mechanical puzzle is constructed is not easy, and it’s a place where many authors fall down on the job.

In his excellent essay “The Craft of Adventure,” Graham Nelson points out a related pitfall ― the in-joke puzzle. You may know what scatological phrase is suggested by using the Greek letters in the name of a certain fraternity as an acronym, or that Petrarch wrote sonnets about a woman named Laura, or the month for which the birthstone is topaz (it’s November), but it’s unlikely your players will make the connection.

In writing your game, it’s vital that you think carefully about the design of your puzzles.

First, have you given the player enough information to enable her to solve the puzzle? Remember: Something that’s obvious to you (the author) may be mystifying to anyone who can’t read your mind.

Second, have you considered and built into your game all of the commands you can think of that a player might use while working on a puzzle? Almost as bad as guess-the-verb puzzles are misleading responses from the parser. Here’s an example:

```
>hit guard
Violence isn’t the answer to this one.

>hit guard with stick
You smack the guard in the head with the stick, and he goes down like a sack of potatoes. Congratulations! Now you can steal the jewels from the vault!
```

Inform’s default response to HIT GUARD is just plain wrong in this case, because violence _is_ the answer to this one.

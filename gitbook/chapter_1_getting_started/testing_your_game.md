## Testing Your Game {#testing-your-game}

Testing a game, or any other piece of software, happens in two stages. In the first (alpha) stage, you test your work as you’re developing it. The best way to do this is to write the game one small piece at a time. For instance, when you add a couple of new rooms (as explained in Chapter 2), click the Go! button to run the game and try walking back and forth from the new rooms to the rooms that were already in place. Even with something as simple as adding rooms, it’s possible to make a mistake in the compass directions or inadvertently create a room when you think you’re creating a door, so you need to test your work.

If you add a dozen rooms, a dozen pieces of scenery, and a machine the player can operate and _then_ run the game, you’re far more likely to miss a bug than if you test a little bit at a time. Worse, you may find yourself staring at a screen full of compiler error messages and have to spend an hour figuring out where your work went astray.

![](../assets/graphics44.jpg)

But even when you test as thoroughly as you possibly can while developing the game, you will miss dozens of awful bugs. This is a promise.

In the second (beta) stage of testing, you enlist the aid of a few industrious volunteers, who _beta-test_ your game before it’s released and send you reports of any bugs they spot. Good beta-testing won’t transform an awful game into a great one, but it can definitely turn an awful game into an okay game, or turn a decent game with deep problems into a great game. (But only if you fix the issues that your testers find. That goes without saying.)

Always thank your beta-testers for sending you their bug reports! And even if you think they’re wrong, don’t argue with them. Like everyone else who plays your game, they’re entitled to an opinion, and even from a wrong-headed opinion, you may be able learn useful lessons.

Encourage your testers to use Inform’s handy transcript feature (not to be confused with the Transcript in the Inform IDE). At the beginning of each play session, they should type the command TRANSCRIPT. This will open a file dialog box in which they’ll be able to specify a name for a script (.scr or .log) file. This file will capture everything that happens in the play session. They can then attach the transcript file to an email and send it to you. In effect, you’ll be able to “watch over their shoulder” while they play the game. This is incredibly useful — you’ll learn a lot about what commands they try to use and what objects they’re interested in examining.

Note that this feature doesn’t work in the Inform IDE. It only works when the game is loaded into a separate interpreter.

Some IF interpreter software may wipe out a running transcript if your game ever clears the screen. If you employ screen-clearing for dramatic purposes between scenes, you need to test what happens in several interpreters (and if possible on both Mac and Windows interpreters) before sending the game to your testers. Or ask them to test it, and tell them how to do so.

Traditionally, IF beta-testers include comments in their transcript by starting a command line with an asterisk. For instance, you might find a line in the transcript that reads like this:

```
>* The room description mentions the vase on the pedestal, but I already broke the vase.
```

By default, Inform will respond to a line like this by saying, “That’s not a verb I recognize.” While not an actual problem, this message soon gets annoying, since the tester is, after all, doing something sensible — namely, giving you a comment. What we’d like would be for Inform to respond with something like, “Comment noted.” Fortunately, this is easy to fix. Copy the following code into your game:

```inform7
Commenting is an action out of world applying to one topic. Understand "* [text]" as commenting.

Carry out commenting:
        say "Comment noted."
```

The details of this code (the definition of the action and the use of a Carry Out rule) are covered in Chapter 4. A slightly more flexible way to get the same result is shown in Example 403, “Alpha,” in the Documentation. However, the regular expression matching used in that example doesn’t match the asterisk character. To allow the tester to use asterisks, as shown above, we would need to edit the code in the example slightly, like this:

```inform7
After reading a command (this is the ignore beta-comments rule):
    if the player's command matches the regular expression "^\p" or the player's command matches the regular expression "^\*":
        say "(Noted.)";
        reject the player's command.
```

With this code in place, your testers can flag their comments with a \*, !, ?, or : (or, for that matter, a ??? or !!!), either in a way that signals what type of comment they’re making, or just for fun. (**Note:** If you’re copying this code from the PDF version of the _Handbook,_ see the sidebar _Copying Example Code_ [here](../chapter_2_rooms_&_scenery/scenery.md#the-names-of-things).)

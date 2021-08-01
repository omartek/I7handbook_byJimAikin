## Using the Debugging Commands {#using-the-debugging-commands}

Inform includes a good set of commands that can be used for speeding up your testing process and tracking down bugs in your game. These commands are available only during the development process; when you release your finished game, other players won’t be able to use them. These commands don’t actually find bugs; what they do is help you see what’s going on in your game while it’s running, and/or take shortcuts that will speed up the testing process.

The commands you can use while your game is running in the Inform IDE include ACTIONS, RULES, PURLOIN, GONEAR, and SHOWME. Also, for testing a series of commands quickly, you can write a TEST ME script. The Replay button can be used to rerun your most recent sequence of commands, which is a very useful way to find out if you’ve succeeded in fixing a problem that you had in the last run-through. The Skein window contains all of your earlier run-throughs, and you can use it to replay just about any series of commands you used earlier.

With the PURLOIN command, you can instantly “grab” any object in your model world. Objects in distant rooms and locked containers can be purloined — and you can also purloin things that can’t be picked up at all in the ordinary way, such as people and scenery. There’s no reason to purloin people or scenery, other than for fun. But by purloining the rusty iron key that’s hidden in the oak cask in the wine cellar, you can quickly test whether the key works to unlock the door of the princess’s chamber. You don’t need to go down to the wine cellar and break open the cask; just PURLOIN the key.

The GONEAR command provides instant transportation to any location in your game. With a large game, one that includes dozens of rooms, GONEAR will save you hours of work. Just pick an item of scenery in the room you want to be transported to, and GONEAR the scenery item.

When using PURLOIN and GONEAR to bypass part of the process that your players will go through, you need to be aware that you can get the game into an unusual state — a state that your players will never encounter. On rare occasions this can lead you to think your code has a bug that isn’t there at all. For instance, let’s suppose you’ve programmed a ghost to follow the player around the haunted castle. If you use GONEAR to pass magically through a locked door, the ghost quite likely won’t be able to follow you.

![](../assets/graphics45.jpg)

The ACTIONS command causes Inform to print out the action that’s being triggered when you type a command. This can be useful if you aren’t getting the results you expect from a command.

The SHOWME command (see **p. 2.7** of the Documentation, “The SHOWME command”) prints out the current state of any object in the model world. SHOWME SHOES, for instance, will print out all of the data associated with the shoes object. When you start writing objects that can get into several different states (for instance, a goblet of wine that can be poisonous or safe), you can use SHOWME GOBLET after dropping the tablets into the goblet to see if the goblet has switched to the state that it’s supposed to.

As explained on **p. 11.4** of _Writing with Inform_, “The showme phrase,” the word showme can be used to add debugging code to your game. When the game is running, if a line with a showme phrase is reached, you’ll see a message in the game window giving whatever information you’ve put in the phrase. I’m not convinced that this is very useful, however. A better method is described on **p. 2.9**, “Material not for release.” After marking a section of your code as not for release, you can put anything you like in that section, secure in the knowledge that it will be available only to you (and to your testers, if you choose). For example, if the hunger of the player character is a numerical value that changes during the game, and you want to keep an eye on it, do this:

```inform7
Section - Not for Release

Every turn:
        say "The hunger of the player is now [hunger of the player].""
```

It’s not always convenient to put this type of game-state monitoring printout code in its own section, however. Another technique is suggested below, in the section “Another Way to Debug.”

More about commands you can use within the game panel while testing your work: If you’re using scenes in your game (see Chapter 7), the SCENES command can be used to show which scenes are currently running.

The TEST ME command (see **p. 2.8** of the Documentation, “The TEST command”) gives you a quick way to run through a series of commands. To start with, define the series of commands you want to use in your game, like this:

```inform7
Test me with "open suitcase / unlock suitcase with rusty key / open suitcase / search suitcase / take dynamite / light match / light dynamite with match / z / z / z".
```

After compiling your game, when you type TEST ME the game will automatically run through this entire sequence of commands, in order. When you’re testing complex puzzles over and over, this will save you lots of typing. The word “me” is used a lot (probably because it’s reminiscent of a scene in _Alice in Wonderland_), but it’s not necessary. You could just as easily do it this way, writing two or more separate tests and then, if you like, writing a TEST ME command that nests some or all of the other tests:

```inform7
Test suitcase with "open suitcase / unlock suitcase with rusty key / open suitcase / search suitcase".
Test dynamite with "take dynamite / light match / light dynamite with match / z / z / z".
Test me with "test suitcase / test dynamite".
```

Now the commands TEST SUITCASE and TEST DYNAMITE can be used independently, or they can be combined by typing TEST ME.

The RULES command can be used while testing your game to find out what rules Inform is using to process other commands. This is a fairly advanced technique — the first few times you try it you may not understand what you’re seeing — but it can sometimes be very useful. If the game is producing an output that you don’t want, you may be able to figure out what rule is producing that output by using RULES and then trying the command that isn’t working correctly. Most often, the last rule that is displayed before the offending output text is the rule that’s producing the text.

### Another Way to Debug {#another-way-to-debug}

One of the easiest traditional ways to debug a computer program is to add print statements. A print statement (which in Inform would be in the form of a “say” statement) prints a text output to the screen. You can put whatever you want in a print statement. For instance, you could do something like this:

```inform7
To demolish the dungeon:
        say "Now entering the dungeon-demolishing code.";
        [other lines of code would go here...]
```

The “say” line doesn’t do anything in your game; it just enables you to test that your code is actually running the “demolish the dungeon” routine when you think it’s supposed to.

Rather than just print out a bare “now this is happening” statement, you could write a testing “say” line that would give you specific information about other things that are going on in the game. Let’s suppose, for instance, that you want the dungeon to be demolished only if the player is carrying the detonator — but for some reason it appears that the player is able to demolish the dungeon even while not carrying the detonator. In that case, you might want to check the player’s inventory while printing out your debugging message:

```inform7
To demolish the dungeon:
        say "Now entering the dungeon-demolishing code. The player is currently carrying [a list of things carried by the player].";
        [other lines of code would go here...]
```

The thing to be careful of with this technique is that you might accidentally leave a debugging print statement in the released version of your game. Erik Temple has suggested a neat way to dodge this danger, however. This uses a bit of inserted Inform 6 code, an advanced technique that is mentioned only briefly in this _Handbook,_ [here](../chapter_10_advanced_topics/what_does_inform_6_have_to_do_with_inform_7#what-does-inform-6-have-to-do-with-inform-7). But since we’re on the topic of debugging, here’s how to do it. First, add the following lines to your game, entering them carefully (the spaces are important):

```inform7
Use inline debugging.

Use inline debugging translates as (- Constant INLINE_DEBUG; -)

To #if utilizing inline debugging:
        (- #ifdef INLINE_DEBUG; -)

To #end if:
        (- #endif; -)

To debug (T - a text):
        #if utilizing inline debugging;
        say T;
        #end if.
```

Having done this, you can now write any debugging print statements that you add to your game’s code like this:

```ìnform7
        debug “--Now entering the dungeon-demolishing code. The player is currently carrying [a list of things carried by the player].]";
```

The lines beginning with # can be used to do other things besides saying texts, though this is probably less useful. For instance:

```inform7
Instead of jumping:
        say "You jumped!";
        #if utilizing inline debugging;
        now the player carries the rutabaga;
        #end if.
```

You might use this technique as a tricky way of resetting in-game objects (such as a locked door) to a desired state in order to test them repeatedly.

When you’re done debugging and ready to release your game, simply comment out the line “Use inline debugging” before compiling for release, and all of the debug code will disappear from the released version of the game.

## Long Names

Normally, Inform looks only at the first nine letters in each word. The rest of the letters are ignored. This is true both for the names of things in your code and for the words in commands that the player types. Normally nine letters are plenty. (In the very first text-based games, only the first five or six letters in the player’s commands were read, and six letters weren’t really enough.) But as **p. 3.1** (“Descriptions”) of the Documentation points out, if you happen to put a superhero and a superheroine in the same room, the player will quite likely get the wrong result from the command KISS SUPERHEROINE.

In fact, the confusion can get deeper than that — unlikely, but possible. Let’s suppose that for some bizarre reason you’ve created the following four objects:

The player carries a superheroism, a superheroine, a superheroich, and a superheroidiot.

Here’s the result when the player tries to take inventory:

```
>**i**
You are carrying:
  four
```

Inform has created four indistinguishable objects, because it was only looking at the first nine letters.

There are two ways to get around this problem, if you ever need to. The easy way requires compiling to Glulx. If you’re not already compiling your game to Glulx, go to the Settings page in the Inform IDE and click the Glulx button. Then add the following line near the top of your source:

```inform7
Use DICT_WORD_SIZE of 12.
```

Now the player will be able to use both SUPERHERO and SUPERHEROINE in commands, and Inform will be able to tell the difference. You can use as large a number as you’d like, but if your game is written in English, it’s hard to see how you would ever need more than the first 12 letters of each word.

If you need to compile to the Z-machine standard (possibly because you want your game to be playable on handheld devices), you won’t be able to change the value of DICT_WORD_SIZE, so you’ll need to resort to a little trickery. The next example is a stripped-down version of some code I used in my game “A Flustered Duck.” Some leprechauns are having a picnic in a meadow, and there’s also a single leprechaun (with whom the player can converse) wandering around playing a fiddle. The trick is, we’re going to use words shorter than nine letters, but allow both the player’s input and the game’s output to use the longer words.

```inform7
After reading a command:
        let N be text;
        let N be the player's command;
        replace the regular expression "leprec" in N with "lpc";
        change the text of the player&#039;s command to N.

The Grassy Knoll is a room. "Some leprechauns are having a picnic here. One leprechaun is sauntering around playing a sprightly tune on a fiddle."

Some lpchauns are scenery in the Grassy Knoll. The description is "They're enjoying their picnic." The printed name of the lpchauns is "leprechauns".

The lpchaun is a man in the Grassy Knoll. The description is "He's playing a fiddle." The printed name of the lpchaun is "leprechaun".
```

The first block of code strips a few letters out of the player’s commands. If the player types X LEPRECHAUN, the game will see the command as X LPCHAUN. Then we use Inform’s handy printed name property so that the object whose real name is lpchaun will be displayed as “leprechaun”, and similarly for the lpchauns.

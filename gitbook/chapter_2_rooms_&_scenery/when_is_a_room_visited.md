## When Is a Room “visited”?

In Chapter 1 we introduced the idea of verbose and brief mode. When a game is in verbose mode, the text of each room’s description property is printed each time the player enters the room. In brief mode, however, the description is printed only the first time the player enters a room. Thereafter, the description is printed only if the player uses the LOOK command. (Note that other aspects of the room’s full description, namely a list of the non-scenery objects that are in the room, will always be printed when the player enters a visited room, even if the game is in brief mode.)

At the beginning of the game, only the room where the player character starts the game is marked as visited. All other rooms are unvisited. What’s interesting is that a room is marked as visited only _after_its description property is printed for the first time. This fact allows us to change the room description after the first time the player reads it:

```inform7
The Throne Room is north of the Entry Hall. "This high-vaulted chamber is grandiose in the extreme. [if unvisited]Your first sight of its magnificence quite takes your breath away. [end if]Each of the dozens of richly woven tapestries lining the walls surely cost more than all of the shabby hovels and mangy livestock in the humble village where you were born."
```

Here, the sentence about the view taking your breath away will appear only the first time the Throne Room is seen.

If the game is in superbrief mode, the description property won’t print even on the player’s first visit. This mode is not used by most players, because room descriptions generally contain useful information! But it’s important to understand that you, the author, don’t get to control whether the player will see the wonderful room descriptions you’ve written.

Or rather … there’s a way to control it, though it would be rude. Let’s suppose that something happens in a room in the course of the game that changes a room so drastically that you’d like to change both its description and its printed name. Perhaps there has been an explosion in the kitchen. The actual name of the room object won’t change — it’s still called Kitchen in the source code. But now we want it to be shown in the game’s output as “Ruins of the Kitchen”. This is easy. As part of the code that produces the explosion (whatever that might be), we write this:

```inform7
now the printed name of the Kitchen is "Ruins of the Kitchen";
now the description of the Kitchen is "About five tons of icky cake batter have splattered everywhere!"
```

The existence of the BRIEF and SUPERBRIEF commands, however, means that you can’t be certain your players will ever read about the cake batter. As part of your explosion in the kitchen, then, you could include, “now the Kitchen is unvisited;”. But if the player has cavalierly switched to superbrief mode, that won’t work: They still won’t see the new description. Arguably, this is their problem, not yours. But if you find it an insupportable intrusion on your authorial prerogatives, you can get rid of brief and superbrief modes entirely, forcing the player to see the complete room description each time a room is entered. Here’s how to do it:

```inform7
Use full-length room descriptions.
Understand the command "brief" as something new.
Understand the command "superbrief" as something new.

Mode-change-refusing is an action out of world, applying to nothing. Understand "brief" and "superbrief" as mode-change-refusing.

Carry out mode-change-refusing:
        say "Sorry -- this game is always in verbose mode."
```

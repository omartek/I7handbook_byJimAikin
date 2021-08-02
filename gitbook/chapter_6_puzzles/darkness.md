## Darkness {#darkness}

The need to bring a light source into a dark room or rooms is a puzzle that dates clear back to “Adventure,” which of course was set in a system of caves. See the section on “Dark Rooms” in Chapter 2, [here](../chapter_2_rooms_&_scenery/dark_rooms.md#dark-rooms). To solve a dark room puzzle, the player has to find and carry an object that provides light. Today, most rooms in most games are lighted by default, but dark rooms still show up in quite a few games. The light source that’s needed may be unusual, or may last for only a limited number of turns — a burning match, for instance — making the dark room a timed puzzle. (See “Timed Puzzles,” below.)

A variant of the dark room puzzle is a dim room, in which you can see some things, probably large ones, but not small things. You might be unable to read written materials in the dim room, for instance.

Objects dropped in dark rooms can’t be picked up again. This fact requires careful thought; it’s possible to make your game unwinnable without meaning to — for instance if the player drops the matches in the dark room before finding the candle. If you don’t want to allow the game to become unwinnable, you’ll need to write a rule that will prevent this from happening:

```inform7
Instead of dropping the candle:
        if the player is in a dark room:
                say "Better keep your hands on the candle for now. You may need it later.";
        otherwise:
                continue the action.
```

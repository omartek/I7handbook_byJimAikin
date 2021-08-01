## Seemingly Identical Rooms {#seemingly-identical-rooms}

Once in a while, you might want to design an area of the map in which there are several rooms that have the same name and description (such as “You are in a maze of twisty little passages, all different.”). Internally, in your code, each of your rooms has to have a unique name of its own. But it’s easy enough to give several rooms the same printed name and description:

```inform7
Land1 is a room. "The landscape stretches out to the horizon on all sides." The printed name of Land1 is "Landscape".

Land2 is south of Land1. "The landscape stretches out to the horizon on all sides." The printed name of Land2 is "Landscape".

Land3 is west of Land1. "The landscape stretches out to the horizon on all sides." The printed name of Land3 is "Landscape".
```

...and so on. To the player, all of these rooms will initially appear to be identical. But as in the original game of Adventure, from which the line about twisty little passages is borrowed, the player can easily drop a different object in each room and then draw a map based on the locations of the various objects and the routes between them. When I find myself (against my better judgment) designing a puzzle of this sort, I usually try to come up with a plausible reason why the player character wouldn’t want to drop anything, such as, “Better not. You might never be able to find it again.” This at least forces the player to come up with a fresh approach to mapping the region. It’s not a very original puzzle, but you might be tempted to try something of the sort, so it’s worth mentioning.

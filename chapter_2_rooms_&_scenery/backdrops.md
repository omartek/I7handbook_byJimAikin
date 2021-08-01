## Backdrops {#backdrops}

Rooms in Inform are not built out of anything — they’re just empty, featureless containers that you can move objects into and out of. In particular, you might expect that a room would have a ceiling, walls, and a floor. But if you try X CEILING, X FLOOR, or X WALL in your game, you’ll be told, “You can’t see any such thing.” Likewise, in an outdoor setting, X SKY and X GROUND won’t work. Most players will probably understand this convention, and won’t even think to try interacting with the walls, ceiling, and floor. But if you mention a wall, ceiling, floor, sky, or ground in the room description, creating it as scenery would be a polite thing to do, since players will usually try to examine (or pick up) anything that’s mentioned.

Scenery is always in one specific room, but Inform also provides a special kind of scenery called a _backdrop._ A backdrop object is unusual because it can be in several places at once.

An easy way to add a little realism to your game is to use backdrops to create sky, ground, ceiling, floor, and so on only where they’re needed:

```inform7
The sky is a backdrop. "A clear and cloudless blue." The sky is in the Great Outdoors.
The ground is a backdrop. "It&#039;s rather dirty.” Understand "dirt" as the ground. The ground is in the Great Outdoors.
```

Now if the player types X SKY in any room in the Great Outdoors, the game will reply, “A clear and cloudless blue.” That’s a definite improvement! (Note that “The description is” is not required for the descriptions of backdrops.) As we add indoor rooms, perhaps in a castle, they won’t be in the Great Outdoors region, so a player who tries X SKY while in the castle will be told, very appropriately, “You can’t see any such thing.”

Backdrops are more versatile than you might expect. A backdrop could be used, for instance, to create a river that’s present in several rooms. In one game I wanted a windowsill (a supporter — see p. 99) that could be reached from both inside and outside the room. At Emily Short’s suggestion, I created the window as a backdrop, so that it could be in two rooms at once, and then made the windowsill a part of the window.

### Removing a Backdrop {#removing-a-backdrop}

Getting rid of a backdrop entirely during play is easy. If we’ve created, for instance, some thick fog, when the player does something to cause the wind to blow, we can write:

```inform7
remove the fog from play;
```

Removing a backdrop from certain rooms while leaving it in other rooms is slightly tricky, however. Inform has no command for this, but we can create a routine that will do it. What we need to do is give all of the rooms where the backdrop is to be found a property. Since we’re going to create some fog, we’ll allow rooms to be foggy or not foggy. We’ll also give the player a giant bellows. Pumping the bellows will dispel the fog, but only from the current room.

```inform7
A room can be foggy or not foggy. A room is usually not foggy.

The Desolate Moor is a room. "A gloomy treeless waste stretches out on all sides[if the fog is in the Moor], but you can&#039;t see very far, because the fog is closing in[otherwise]. You can see a path that extends north and south from here[end if]." The Desolate Moor is foggy.

The Haunted Grove is north of the Desolate Moor. "Thin, widely spaced trees of a mournful character surround you[if the fog is in the Grove]. It's difficult to see where you might go from here, because the fog presses close among the trees[otherwise]. A path leads south out of the grove[end if]." The Haunted Grove is foggy.

The Bog is south of the Desolate Moor. "The ground here is quite moist[if the fog is in the Bog], and the fog is thicker[otherwise]. A path extends out of the bog to the north[end if]." The Bog is foggy.

The thick gray fog is a backdrop. The description is "Tendrils of gray fog drift across the land."
When play begins:
        move the fog backdrop to all foggy rooms.

The player carries some giant bellows. The indefinite article of the giant bellows is "a".

Pumping is an action applying to one thing. Understand "pump [something]" as pumping.
Check pumping:
        say "[The noun] [are] not something you can pump."

Instead of pumping the giant bellows:
        if the location is foggy:
                say "As you pump the bellows with great vigor, the fog blows away!";
        otherwise:
                say "You've already dispelled the fog here.";
        now the location is not foggy;
        update backdrop positions.
```

The crucial thing in this example is the Instead rule. It makes the location not foggy, and then updates the backdrop positions (see **p. 8.8** in _Writing with Inform_, “Moving backdrops”).

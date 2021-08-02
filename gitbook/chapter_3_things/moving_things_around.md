## Moving Things Around {#moving-things-around}

You can expect that during the game, the player will pick things up, carry them around, and drop them. But sometimes you need to move them yourself, in your own code. For instance, if the player rubs the magic lamp, you would probably want to move the genie into the room. The keyword for doing this is “now”:

```inform7
Instead of rubbing the lamp:
        if the genie is off-stage:
                now the genie is in the location;
                say "Shazam! A genie appears!";
        otherwise:
                say "You make a small squeaking noise by rubbing the lamp."
```

In this case, “the location” refers to the room where the player is. If you need to move an object to a container or supporter, it’s usually easiest to refer to the container or supporter by name:

```inform7
now the knockwurst is on the plate;
```

But sometimes you may not know exactly where the object should show up. That can happen, for instance, if you’re transforming an old shoe into a jewelled crown. In this case the shoe could be almost anywhere, so you need to figure out where it is, store that data, and then use the data to move the jewelled crown onstage:

```inform7
Instead of the player rubbing the lamp:
        if the holder of the old shoe is not nothing:
                let H be the holder of the old shoe;
                move the jewelled crown to H;
                remove the old shoe from play;
                say "You rub the old lamp. Squeak, squeak[if the player is in the location of the jewelled crown]. The old shoe turns into a jewelled crown![else].";
                else:
                say "You rub the old lamp. Squeak, squeak."
```

As the code above shows, you can’t move something off-stage by saying “now the X is off-stage”. The way to do it is to say “remove the X from play”. This code also does a little testing to make sure that the old shoe hasn’t already been moved off-stage. If we didn’t test that, then rubbing the lamp a second time would produce a run-time error, because the game would have tried to move the jewelled crown to nothing. As the Inform 6 _Designer’s Manual_ emphasizes, nothing is not a thing. That’s why we have to use a special phrase (“remove the old shoe from play”) to put the shoe nowhere.

This code also suggests a way of getting the proper vertical spacing in the output. Notice the way the punctuation and conditional clauses (“[if the player]”) are organized. Doing it a different way will produce an ugly, non-standard output.

For an example of how to move a bunch of indistinguishable objects at once using a loop, dollar bill example [here](.//chapter_9_phrasing_&_punctuation/values.md#values)).

I once had a beginning student try to add an item to the player’s inventory (for a discussion of inventory, see below) by saying exactly that:

```inform7
add the sword to the player's inventory. [Error!]
```

You might think that would work, but it won’t, first because there is no container in the model world called “inventory” and second because “add” refers to an arithmetic operation, not to moving an object around in the world. The way to give the sword to the player as an item being carried is this:

```inform7
now the player carries the sword.
```

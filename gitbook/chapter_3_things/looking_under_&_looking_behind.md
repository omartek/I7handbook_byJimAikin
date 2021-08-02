## Looking Under &amp; Looking Behind

Experienced IF players know that authors like to hide things under other things — under a bed, for example. When a player enters a room and sees a bed, he’s bound to try LOOK UNDER BED before very long. Inform’s default response is, “You find nothing of interest.” Creating a non-default response is easy:

```inform7
Instead of looking under the bed:
say "Nothing but dust bunnies."
```

On **p. 6.6** of the _Recipe Book_ you’ll find several ideas about how to hide things under other things. If we want to, we can have the player “find” something by moving it from off-stage into the room, or directly into the player’s inventory, like this:

```inform7
The odd sock is a thing. The odd sock can be found. The odd sock is not found.

Instead of looking under the bed:
        if the odd sock is found:
                say "There's nothing else of interest under there, just a few dust bunnies.";
        otherwise:
                now the odd sock is found;
                now the player carries the odd sock;
                say "Under the bed you find an odd sock, which you retrieve."
```

This works nicely, up to a point. For your first game, it may be all you want or need. But there are at least two potential problems lurking here (leaving aside the possibility that the player will try to pick up the dust bunnies and learn that she can’t see any such thing). First, it won’t be possible to put anything (including the sock) under the bed:

```
>put sock under bed
I didn't understand that sentence.
```

And second, if your game limits the number of items the player can carry at once, giving the sock to the player automatically (as shown above) may cause the player to be carrying more than the allowed number of things. I’ve found that this can trip up Inform’s process of automatically inserting excess items into the player’s holdall (a handy bag for carrying excess inventory).

This is a good reason for moving the sock into the room rather than adding it directly to the player’s inventory. But then the player has to TAKE SOCK as an extra command, which is a bit annoying. If the player finds the sock, shouldn’t picking it up happen at the same time?

Another way to hide the odd sock under the bed is to include Underside by Eric Eve. This is a handy extension. Once this extension has been included in your game, hiding the sock under the bed is easier:

```inform7
The double bed is a supporter in the Bedroom. The double bed is fixed in place. An underside called under#bed is part of the double bed.

The odd sock is in under#bed.
```

The name “under#bed” is not special; it’s just a good idea to use a name that the player is not likely to type.

When an object is in an underside, it won’t be mentioned in a room description, and it won’t be included in the object list if the player tries to TAKE ALL.

There is no extension for hiding things behind other things. Most often, if you want to do this, you’d be hiding something behind a picture on the wall, or behind a couch, and the way to let the player find it would be with the command TAKE PICTURE or MOVE COUCH. Inform does not include looking behind as an action, though. Here’s how to set that up:

```inform7
Looking behind is an action applying to one thing and requiring light. Understand "look behind [something]" as looking behind.

Check looking behind:
        say "You find nothing interesting behind [the noun]."

Instead of looking behind the couch:
        say "I's jammed up against the wall. In order to see what's behind it, if anything, you'll need to pull it out from the wall."
```

Pulling something away from the wall would require another action, as well as a way to test the position of the couch within the room. Is it against the wall, or has it been moved? Let’s add that possibility:

```inform7
The couch is in the Living Room. The couch can be moved or not moved. The couch is not moved. The description is "An overstuffed couch stands [if not moved]against the wall[otherwise]in the middle of the room[end if]."
Instead of pushing the couch:
        try pulling the couch.
Instead of pulling the couch:
        if the couch is moved:
                say "It's already out in the middle of the room.";
        otherwise:
                now the couch is moved;
                move the odd sock to the Living Room;
                say "As you wrestle the couch out into the middle of the room, you find an odd sock behind it."
```

Allowing the player to push the couch back against the wall would be a bit more complicated. For one thing, you’d have to make sure that the odd sock wouldn’t keep popping back into the room each time the couch was moved.

A simpler solution might be to implement the LOOK BEHIND action and then simply drag the hidden object into the game from offstage when the player uses the command:

```inform7
The Library is a room. "A beautiful tapestry hangs from the wall here."

A beautiful tapestry is scenery in the Library. "Sir Lancelot is depicted in vivid DayGlo stitchery. He seems to be riding on a sheep."

The rusty dagger is a thing. The description is "Though mottled with rust, it looks quite sharp." The dagger can be discovered or undiscovered. The dagger is undiscovered.

Looking behind is an action applying to one visible thing and requiring light. Understand "look behind [something]", "peek behind [something]", and "search behind [something]" as looking behind.

Check looking behind:
        say "There's nothing of any interest behind [the noun]."

Instead of looking behind the tapestry:
        if the dagger is undiscovered:
                now the dagger is in the Library;
                now the dagger is discovered;
                say "As you disturb the tapestry, a rusty dagger falls out from behind it and lands on the floor.";
        otherwise:
                say "You find nothing else of interest behind the beautiful tapestry."
```

If you do it this way, you might want to add the following, as a courtesy to the player who tries MOVE TAPESTRY or SHAKE TAPESTRY:

```inform7
Instead of pushing the tapestry:
        try looking behind the tapestry.

Shaking is an action applying to one visible thing and requiring light. Understand "shake [something]" as shaking.

Check shaking:
        say "Agitating [the noun] has no visible effect."

Instead of shaking the tapestry:
        if the dagger is undiscovered:
                try looking behind the tapestry;
        otherwise:
                say "A little dust billows out."
```

This is the first place in the _Handbook_ where we’ve added new actions (looking behind and shaking). In Chapter 4 you’ll learn much more about how to do this.

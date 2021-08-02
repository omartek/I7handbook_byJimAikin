## Body Parts {#body-parts}

Giving your characters body parts is not always necessary, but if the character’s description mentions something prominently (Janet’s blue eyes, the duke’s hawklike nose, or whatever), you can easily use Inform’s ability to create parts of objects (as discussed in Chapter 3 of this _Handbook_) to make the body parts. In some games, you might want to give all of your characters body parts. In this case, you would make the part a kind of thing, like this:

```ìnform7
The Living Room is a room.

A nose is a kind of thing. A nose is part of every person. The description of a nose is usually "Seen one nose, seen [']em all."

Susan is a person in the Living Room.

The description of Susan's nose is "It has a cute upward tilt." Understand "cute" as Susan's nose.

The description of your nose is "You can't see much of it, as you're behind it."
```

The only odd thing about this is that you can’t say “The description of the player’s nose”. Or rather, you can; it will compile; but it won’t work. Instead, you have to say “your nose”. Inform will understand that the player can then refer to this object as “my nose”.

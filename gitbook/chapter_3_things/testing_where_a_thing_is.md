## Testing Where a Thing Is

In writing a game, it’s often very useful to be able to test where something is. If the time bomb is in the suitcase, for instance, and the player is carrying the suitcase or just in the room with the suitcase, we might want to print out “You hear a faint ticking noise” once every few turns.

Inform has several words for describing and testing where things are. It’s important to use the right word, because if you use the wrong one, your test may fail, causing a bug in your game. These words are ways of describing **relations**. Relations (see **p. 13.3** of _Writing with Inform_, “What are relations?”, or [here](../chapter_10_advanced_topics/relations.md#relations) of the _Handbook_) are an important and versatile concept in advanced Inform programming. The relations that relate to where things are located are the containment, support, incorporation, carrying, wearing, and possession relations.

Internally, your game has a _containment hierarchy_. This is a fancy way of saying that Inform knows when object A is inside of or on object B, while object B is inside of or on object C, while object C is … and so on. The relationships between objects in the hierarchy will be one or another of these relations. For instance, if object A is inside object B, they are related by the containment relation.

A room is always at the top of the hierarchy: it’s not possible for one room to be inside another room — though we can fake this easily by creating a new room that’s inside from another room. In this case, Inform understands that “inside” is just another direction, like north or down. This fact is mentioned on **p. 3.2** of _Writing with Inform_, “Rooms and the map.”

If the aspirin tablet is in the pill box, the pill box is in the suitcase, the leather suitcase on the table, and the old oak table in the Dining Room, the containment hierarchy would look like this:

Dining Room
        old oak table
                leather suitcase
                        pill box
                                aspirin tablet

The words “in” and “on” mean just what you think they should — and they refer only to things that are _directly_ in a container (or room) or on a supporter. In the hierarchy shown above, the table is in the Dining Room, but the leather suitcase is _not_ in the Dining Room. Likewise, the suitcase is on the table, but the pill box is _not_ on the table. Because Inform distinguishes “in” from “on,” the table is not “on” the Dining Room, and the suitcase is not “in” the table.

We can test whether the player (or another character) carries an item. Like on and in, “carries” only refers to things that the player carries directly. If the player carries the pill box, and the aspirin tablet is in the pill box, the result of the test “if the player carries the aspirin tablet” will be false.

Inform’s most general term for testing where a thing is is “enclosed by”. In the example above, the aspirin tablet is enclosed by _everything_ above it in the containment hierarchy — the pill box, the leather suitcase, the old oak table, and the Dining room.

We can reverse these terms if we like. We can say, “if the Dining Room encloses the pill box”. This will be true if “if the pill box is enclosed by the Dining Room” is true.

The **location** of a thing is always the room, as **p. 3.25** of _Writing with Inform_ (“The location of something”) points out. In the diagram above, the location of every object (except the Dining Room itself) is the Dining Room.

We can test whether two objects are sitting next to one another — in the same container, on the same supporter, carried by the same person, or in the same room — using the general-purpose term “holder”:

```inform7
if the holder of the pear is the holder of the banana:
```

This condition will be true if they’re both carried by the player, or both in the same basket, or both on the floor of the room. But if the player is holding the basket and the pear, while the banana is in the basket, it will be false.

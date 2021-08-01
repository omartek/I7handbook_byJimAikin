## Duplicate Exits &amp; Twisty Connections {#duplicate-exits-twisty-connections}

Let’s suppose we’ve created a room that’s described like this:

```inform7
The Cellar is down from the Kitchen. "The low ceiling of this little room is festooned with cobwebs, and the floor is dirt. A rough doorway leads east, and the stairs up to the kitchen are built into the north wall."
```

Because we’ve said the Cellar is down from the Kitchen, Inform creates an up/down map connection between the two rooms. But you’ll notice that the room description (in the interest of adding detail) mentions that the stairs are to the north. If the player should try to go north, though, she’ll be told, “You can’t go that way.” This is not too friendly, but it’s easy to fix:

```inform7
Instead of going north in the Cellar, try going up.
```

By the way, Inform insists that we write this as “try going up”, not simply as “go up”. The reason is because there’s no guarantee that the action will succeed. Going up might not work for some reason: Maybe the stairs will collapse, trapping the player in the cellar! That’s why the word “try” is used so often in Inform code.

Sometimes we need to make a one-way connection between rooms. Possibly there’s a chute in the cellar, which the player can go down in order to reach the cavern — but once in the cavern, will be unable to climb back up the chute. It would be friendly to the player to mention that the chute looks a bit treacherous. (This example is similar to one of the first puzzles in Zork, by the way.) There are two ways to do this in Inform.

```inform7
The Cellar is down from the Kitchen. "The low ceiling of this little room is festooned with cobwebs, and the floor is dirt. A rough doorway leads east, and the stairs up to the kitchen are built into the north wall. In the southeast corner is a hole that looks wide enough to enter, but if you climb down it, there’s no guarantee you’ll be able to get back up."

The Spider-Infested Cavern is down from the Cellar. "Spiders! Thousands of them!"Up from the Spider-Infested Cavern is nowhere.
```

Here we’ve created a one-way map connection by telling Inform that the up direction from the cavern leads nowhere. The other way to do it would be with an Instead rule:

```inform7
The Spider-Infested Cavern is down from the Cellar. "Spiders! Thousands of them!"

Instead of going up in the Spider-Infested Cavern, say "The hole is too steep for you to climb back up."
```

The advantage of using an Instead rule is that you can tell the player exactly what the travel problem is.

In the original game of Adventure, some of the rooms were connected not in the normal way, but with “twisty” connections. One of the main puzzles in the game involved figuring out how to draw a reliable map. This type of puzzle is not used much in modern games. For one thing, players find it annoying and not fun. But once in a while you may want to create a connection between two rooms that is a bit twisty rather than straight. For instance, the room description might tell the player, “You can go east around the corner of the building.” To return after going east, you might need to go north. Here’s how to create this type of connection:

```inform7
Deeper in the Cellar is east of the Cellar. "This little room smells awful."
The Cellar is north of Deeper in the Cellar.
West of Deeper in the Cellar is nowhere.
South of the Cellar is nowhere.
```

Notice that we have to tell Inform that after going east from the Cellar, we can’t get back where we started by going west — we have to go north. That’s why the two “nowhere” lines have been added. This makes the model world a little more realistic. It’s also a good idea if you’re including Exit Lister by Eric Eve. This extension will list the exits from every room in the status line — and if a room with only one actual exit shows two exits on the status line, the player may get a little confused.

For a more concise syntax that will produce “dog-leg” connections between rooms, see Example 7 (“Port Royal 2”) in the Documentation. We can do it this way:

```inform7
East of the Cellar is north of Deeper in the Cellar.
```

An even more twisty and confusing map connection is to have one of the exits of a room lead back into the same room. To do that, you would write something like this:

```inform7
East of Deeper in the Cellar is Deeper in the Cellar.
```

### Hallways with Lots of Doors {#hallways-with-lots-of-doors}

A different type of mapping challenge arises when the story calls for a long hallway from which several doors lead off in the same direction. If the hallway runs from east to west, for example, there may be four or five doors that are notionally to the north, and four or five more that are to the south. There are a couple of ways to deal with this challenge, each with its own strengths and limitations.

First, you can break the long hallway up into several separate “rooms” (East End of Hallway, Center of Hallway, and West End of Hallway, for instance), each of which has its own exits to the north and south. If you do this, you’ll probably want to consider what happens if the player drops something large at one end of the hallway and then walks down to the other end. As explained earlier in this chapter, it’s possible to make objects visible from a distance, so this is not a huge challenge, it’s just extra work to set it up.

Alternatively, you can skip (in this one room) the notion of N/S/E/W travel commands. If you give each door a distinctive appearance, you can invite the player to GO THROUGH DOOR 16 as a method of traveling. Here is an example that shows how to do precisely that:

```inform7
The Long Hallway is a room. "The hallway runs from east to west. In the north wall are three doors, numbered 16, 17, and 18." North of the Hallway is nowhere.

Door 16 is scenery in the Hallway. "To the door is nailed a brass number 16." Understand "number" as door 16

Door 17 is scenery in the Hallway. "To the door is nailed a brass number 17." Understand "number" as door 17.

Door 18 is scenery in the Hallway. "To the door is nailed a brass number 18." Understand "number" as door 18.

Room 16 is a room. "You are now in the featureless Room 16 The door is to the south." South of Room 16 is the Hallway.

Room 17 is a room. "You are now in the featureless Room 17\. The door is to the south." South of Room 17 is the Hallway.

Room 18 is a room. "You are now in the featureless Room 18\. The door is to the south." South of Room 18 is the Hallway.

Instead of entering Door 16:
        say "[command clarification break]";
        now the player is in Room 16.

Instead of entering Door 17:
        say "[command clarification break]";
        now the player is in Room 17.

Instead of entering Door 18:
        say "[command clarification break]";
        now the player is in Room 18.

Instead of going north in the Hallway:
        say "You can go through door 16, door 17, or door 18."
```

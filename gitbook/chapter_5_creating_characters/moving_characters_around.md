## Moving Characters Around {#moving-characters-around}

People don’t always stay in one place. In the real world, people do sometimes stay put for long periods of time — for instance, the librarian sitting behind her desk, who won’t leave for hours. Other times, though, people move from one place to another. There are several ways to imitate that behavior in interactive fiction.

A classic effect in the early days of IF was to have an NPC wander at random around the map. This isn’t very realistic, because people usually have reasons for going places, but at least it adds a little variety to the game. An example of an NPC who might be expected to behave this way would be a butler moving from room to room in a large mansion.

In the simple example below, we’ll create a square 3x3 grid of rooms and then create an NPC who wanders at random. If you can’t tell from the code what the map will look like, switch to the Index World tab after compiling the game.

```inform7
A boring room is a kind of room. The description of a boring room is usually "Not much to see or do here."

Room 1 is a boring room. Room 2 is a boring room. Room 3 is a boring room. Room 4 is a boring room. Room 5 is a boring room. Room 6 is a boring room. Room 7 is a boring room. Room 8 is a boring room. Room 9 is a boring room.

Room 4 is south of room 1. Room 7 is south of room 4.

Room 2 is east of room 1. Room 3 is east of Room 2.

Room 5 is east of Room 4 and south of Room 2. Room 6 is east of Room 5 and south of Room 3. Room 8 is east of Room 7 and south of Room 5. Room 9 is east of Room 8 and south of Room 6.

Bob is a man in Room 3.

Every turn:
        let D be a random direction;
        try Bob going D.
```

As a result of the Every Turn rule, Bob will try going some direction or other in every turn, but if no room exists in the random direction, the “try” statement will fail. Bob will stay where he is. If the player is in a room when Bob arrives, the game will report the fact. Likewise, if Bob and the player are in the same room, the game will report when Bob succeeds in leaving. The output might look like this:

```
Room 5
You can see Bob here.

Bob goes south.

>z
Time passes.

>z
Time passes.

Bob arrives from the south.
```

This is okay as far as it goes, but the outputs (“Bob goes south” and “Bob arrives from the south”) are not very interesting. If you turn on rules reporting using the RULES command, you’ll learn that these outputs are coming from the “describe room gone into rule.” You can’t find this rule by searching _Writing with Inform_. Nor is it visible in the Index Rules area. However, you can find it by going to File/Open Extension/Graham Nelson/Standard Rules. It’s more than 60 lines long.

Replacing the entire rule would require quite a bit of tinkering; I wouldn’t want to try it, because I’d probably end up adding bugs. If all we really want is to make your characters’ arrivals and departures a little more interesting, here’s a simple way to do it. Note that this doesn’t handle complex situations, such as when the NPC is in a vehicle.

```inform7
Report someone (called the traveler) going:
        if the traveler is in the location:
                say "[one of]Here comes old [actor] again[or][The actor] saunters up to you[or]The ominous creaking of floorboards announces the arrival of [the actor][at random]." instead;
        otherwise:
                say "[one of]At the sound of a thin scream in the distance, [the actor] dashes away[or]You suddenly notice that [the actor] has wandered off somewhere[or][The actor] evaporates in a thin puff of acrid smoke[at random]." instead.
```

This code doesn’t tell the player which direction the character arrives from or departs to; that would require more tinkering. But now we have a way to add a little variety to the output.

**Page 7.13** in the _Recipe Book_ provides several examples of different ways to move NPCs around. Possibly the most interesting of these is shown in Example 185, “Latris Theon.” Inform includes a path-finding algorithm — a built-in procedure that will allow an NPC to calculate the best route from his or her current location to any other location. Applying this to the example given earlier is not difficult: Replace the last two blocks (“Bob is in Room 3” and the Every Turn rule) with the following code:

```inform7
Bob is a man in Room 3\. The destination of Bob is Room 3\. Persuasion rule for asking Bob to try going vaguely: persuasion succeeds.

Every turn when the destination of Bob is not the location of Bob:
        let the right direction be the best route from the location of Bob to the destination of Bob;
        try Bob going the right direction.

A person has a room called destination.

Understand "go to [any room]" as going vaguely.

Going vaguely is an action applying to one visible thing.

Carry out someone going vaguely:
        change the destination of the person asked to the noun.

Report someone going vaguely:
        say "[The person asked] looks amused, but accepts the commission to go to [the noun]."

Carry out going vaguely:
        say "You're too thoroughly lost."
```

We’ve done a few new things here. First, “A person has a room called destination.” Since Bob is a person, he now has a destination. Initially we make his destination Room 3, so he’s happy to stay where he is. He’s no longer going to wander around at random. Next, we include a persuasion rule, so that Bob will respond to an order to go vaguely. (The persuasion rule will cause BOB, GO TO ROOM 7 to work the way we’d like it to.) The rest of the new code is directly copied from “Latris Theon.”

Notice also the difference between the two Carry Out rules. One applies to _someone_ going vaguely (in other words, not the player character), while the other applies to the PC.

Example 274, “Odyssey,” is on the same page of the _Recipe Book_. This shows how to move an NPC along a route that we’ve created in advance. The NPC’s travel will be interrupted temporarily if the player chooses to interact with her. One refinement I’d suggest adding to this example, if you try it out, would be to define a scene called Athena Traveling. (For more on Scenes, see [here](../chapter_8_time_&_scenes/scenes.md#scenes) and Chapter 10 of _Writing with Inform_.) I would then change the Every Turn rule like this:

```inform7
Every turn when Athena Traveling is happening:
        if Athena is active:
```

This will allow you to keep Athena (or whatever NPC you’re using) in one place until some specific event occurs. For instance, you might do this:

```inform7
Athena Traveling is a scene. Athena Traveling begins when the player carries the laurel wreath.
```

Now Athena will stay put (perhaps lurking in her temple) until the player picks up the laurel wreath. When that happens, she’ll set out on her journey.

The extension called Patrollers by Michael Callaghan provides some extra tools with which to write NPCs who move from place to place.

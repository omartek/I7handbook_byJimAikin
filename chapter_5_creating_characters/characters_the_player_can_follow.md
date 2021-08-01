## Characters the Player Can Follow {#characters-the-player-can-follow}

There are at least two ways (and maybe more) to set up a game so that the player needs to follow another character. First, the NPC may be standing in the room, saying, “Come on, follow me!” or something of the sort, in which case the command FOLLOW BOB would likely be implemented so as to move both the PC and the NPC to whatever room the NPC has in mind. Second, the NPC may just have left the room, and the player may now be wanting to follow the NPC to see whither he is bound.

The second situation is trickier than the first. This is because of the way Inform handles scope. As explained [here](../chapter_2_rooms_&_scenery/creating_your_first_room.md#creating-your-first-room), the player can normally only refer to objects that are in the same room (and also visible — an object in a closed container is invisible, for instance, unless the container is transparent). If the NPC has left the room, he won’t be in scope, so FOLLOW BOB will produce the unhelpful output “You can’t see any such thing.” Well, duh — that was why I wanted to follow him!

Example 302, “Actaeon” (found on **p. 7.13** of the _Recipe Book_), shows how to allow the PC to follow an NPC who has left the room. This example is easy to customize, but it’s worth including some of the code here to point out a couple of features. We’ll start with the setup from [here](../chapter_5_creating_characters/moving_characters_around.md#moving-characters-around), in which Bob is meandering around a featureless grid of nine rooms. This time, though, we’ll start him in Room 1, so the player can start following him immediately.

```inform7
Bob is a man in Room 1.

Every turn:
        let current location be the location of Bob;
        let next location be a random room which is adjacent to the current location;
        if Bob is visible, say "Bob saunters off toward [the next location].";
        move Bob tidily to next location;
        if Bob is visible, say "Bob saunters in from [the current location]."

Following is an action applying to one visible thing. Understand "follow [any person]", "chase [any person]", and "pursue [any person]" as following.

A person has a room called last location.

Check following:
        if the noun is the player:
                say "You run around in circles briefly, but there doesn't seem to be much point in that, so you stop." instead;
        if the noun is visible, say "[The noun] is right here." instead;
        if the last location of the noun is not the location, say "It's not clear where [the noun] has gone." instead.

Carry out following:
        let the destination be the location of the noun;
        if the destination is not a room, say "[The noun] has gone where no one can follow." instead;
        let aim be the best route from the location to the destination;
        say "(heading [aim])[line break]";
        try going aim.

To move (pawn - a person) tidily to (target - a room):
        now the last location of the pawn is the holder of the pawn;
        move the pawn to the target.
```

If you look at the Every Turn rule here, or just try it out in a test game, you’ll find that Bob moves to a new room in every turn. In the examples earlier in this chapter, Bob would choose a random direction every turn — but if there was no room in that direction, he wouldn’t move. The line above, “let next location be a random room which is adjacent to the current location;” causes Bob to choose a random room that actually exists, and move to it.

We have to move Bob in a tidy way, or “tidily” (an ugly word, but useful), so that he’ll keep track of where he was last.

If you comment out the last line in the Check Following rule, the player will be able to follow Bob even after several turns have elapsed. The result may turn out to be slightly unrealistic, however, because the PC won’t necessarily take the route that Bob took. Instead, the PC will choose the best route to wherever Bob happens to be _now._ If Bob has traveled around to the other side of the map — if he left heading south but is now in a room to the north — this code will cause the PC to go north, which is rather odd, and doesn’t accord well with the meaning of the word “follow.” That’s probably why the original code in this example only allows the follow command to be used immediately after the NPC has left the room. Storing an NPC’s entire route, so as to allow the player to follow (perhaps by tracking footprints or dropped breadcrumbs) would be a lot more work, and would probably be unrealistic unless the NPC is leaving a trail of breadcrumbs, so we’ll leave it as a coding challenge for advanced Inform authors.

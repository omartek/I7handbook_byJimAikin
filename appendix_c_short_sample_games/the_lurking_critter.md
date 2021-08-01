## The Lurking Critter {#the-lurking-critter}

This example, which was inspired by an answer that Mike Gentry gave on the newsgroup to a question from S. John Ross, is included principally to show a way of changing the state of an object (the sword) and of reporting that change in certain conditions — namely, if the player is carrying the sword. The idea that the sword glows if the lurking critter is nearby is borrowed from Zork.

We’ll start by creating a checkerboard-like matrix of 16 rooms. This matrix is at least mildly interesting in that the room connections cross one another without intersecting. That is, you can go southeast from Room1 to Room6, or southwest from Room2 to Room5, but the two paths are independent. (Maybe there are arched stone bridges.) Both the player and the lurking critter can move diagonally from room to room as well as orthogonally. The critter will move at random, but only 50% of the time.

```inform7
Room1 is a room. Room2 is east of Room1. Room3 is east of Room2. Room4 is east of Room3.

Room5 is south of Room1. Room6 is east of Room5 and south of Room2. Room7 is east of Room6 and south of Room3. Room8 is east of Room7 and south of Room4.

Room9 is south of Room5. Room10 is east of Room9 and south of Room6. Room11 is east of Room10 and south of Room7. Room12 is east of Room11 and south of Room8.

Room13 is south of Room9. Room14 is east of Room13 and south of Room10. Room15 is east of Room14 and south of Room11. Room16 is east of Room15 and south of Room12.

Room5 is southwest of Room2. Room6 is southwest of Room3 and southeast of Room1. Room7 is southwest of Room4 and southeast of Room2. Room8 is southeast of Room3.

Room9 is southwest of Room6. Room10 is southwest of Room7 and southeast of Room5. Room11 is southwest of Room8 and southeast of Room6. Room12 is southeast of Room7.

Room13 is southwest of Room10. Room14 is southwest of Room11 and southeast of Room9. Room15 is southwest of Room12 and southeast of Room10. Room16 is southeast of Room11.

The lurking critter is a man in Room4.

Brightness is a kind of value. The brightnesses are glowing brightly, glowing faintly, and glowless.

The player carries a sword. The sword has a brightness. The brightness of the sword is glowless. The description is "A trusty critter-sensing weapon[if the brightness of the sword is glowing faintly]. It's glowing faintly[otherwise if the brightness of the sword is glowing brightly]. It's glowing brightly[end if]."
```

This next routine does two things. It always adjusts the sword-glow to reflect the sword’s current proximity to the lurking critter. It then reports a change in the sword-glow — but only if the player carries the sword. I chose to do it this way because in the real world, you’d be less likely to notice a change if the sword were simply lying nearby than if it’s in your hand.

```inform7
To adjust sword-glow to (b - a brightness):
      	let current glow be the brightness of the sword;
      	now the brightness of the sword is b;
      	if b is the current glow:
            		do nothing;
      	otherwise if b is glowless:
            		if the player carries the sword:
                  			say "Your sword is no longer glowing.";
      	otherwise if b is glowing faintly:
            		if the player carries the sword:
                  			say "Your sword glows with a faint blue glow.";
      	otherwise:
            		if the player carries the sword:
                  			say "Your sword is glowing brightly."
```

This next definition is used, rather than the library’s default terminology, “adjacent room,” because room adjacency isn’t considered to exist if two rooms are separated by a door. You might want to add doors to your game.

```inform7
Definition: a room is neighboring if the number of moves from it to the location is 1.
```

And finally, we’ll move the critter (maybe) and adjust the sword-glow:

```inform7
Every turn:
      	if a random chance of 1 in 2 succeeds:
            		let current location be the location of the lurking critter;
            		let next location be a random room which is adjacent to the current location;
            		if the lurking critter is visible:
            			say "The critter [one of]slouches[or]slithers[or]shambles[or]lurches[at random] away.";
            		move the lurking critter to next location;
            		if the lurking critter is visible:
                  			say "A critter [one of]oozes[or]staggers[or]ambles[or]creeps[at random] into the room.";
      	[Whether or not the critter has moved, we need to adjust the sword-glow, because the player may have moved.]
      	if the lurking critter is in the location:
      		      adjust sword-glow to glowing brightly;
      	otherwise if the lurking critter is in a neighboring room:
      		      adjust sword-glow to glowing faintly;
      	otherwise:
      		      adjust sword-glow to glowless.
```

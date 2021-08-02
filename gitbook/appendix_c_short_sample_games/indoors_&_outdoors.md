## Indoors &amp; Outdoors

Inform’s built-in library creates rooms in a basic way. They have no walls, floor, or ceiling. If outdoors, they have no ground or sky. Such objects can easily be created as backdrops. A more serious limitation is that even outdoor rooms are, by default, “sealed containers.” You can’t look from one outdoor room into another and see anything that’s there.

My first thought was to bundle the example game below as an extension, in order to provide these features and a few others for anyone who might find them useful. But I suspect authors will almost always want to customize the implementation in various ways. Since none of the code in the example game is tucked away in an extension, you can easily copy it into your own game and modify it as needed.

If you want to write a realistic outdoor setting, spend some time studying **page 3.4**, “Continuous Spaces and the Outdoors,” in the _Recipe Book_. The examples on that page illustrate some useful techniques. For the present example, we’re going to implement both outdoor and indoor rooms. We’ll start by creating some backdrops and a couple of kinds of room. (Note that to use this code, you will usually need to add a few extra words to each of your existing room definitions, to tell Inform whether the new room is an indoor room or an outdoor room.)

We need a special “check taking” rule for the sky, because by default Inform will respond to the player’s attempt to take a backdrop by saying “That’s hardly portable.” This response works fine for walls, floor, ceiling, and ground, but not for the sky.

```inform7
An outdoor room is a kind of room. An indoor room is a kind of room.

The sky is a backdrop. The description is "A bright and cloudless blue."

Check taking the sky:
        say "You can't touch the sky.";
        rule fails.

The ground is a backdrop. The description is "The ground is a bit uneven." Understand "uneven" as the ground.
The ceiling is a backdrop. The description is "A few cobwebs up there." Understand "cobwebs" as the ceiling.
The floor is a backdrop. The description is "The floor is flat and level."

A backdrop has a direction called wall-direction. The wall-direction of a backdrop is usually up.

A wall is a kind of backdrop.
The east wall is a wall. The wall-direction of the east wall is east.
The north wall is a wall. The wall-direction of the north wall is north.
The south wall is a wall. The wall-direction of the south wall is south.
The west wall is a wall. The wall-direction of the west wall is west.
The description of a wall is "It's vertical." Understand "walls" as the plural of a wall.

A corner is a kind of backdrop.
The northeast corner is a corner. The wall-direction of the northeast corner is northeast.
The northwest corner is a corner. The wall-direction of the northwest corner is northwest.
The southeast corner is a corner. The wall-direction of the southeast corner is southeast.
The southwest corner is a corner. The wall-direction of the southwest corner is southwest.
The description of a corner is "Two walls join here at right angles." Understand "corners" as the plural of a corner.
```

Defining some of the directions as diagonal will become important if the player tries LOOK NORTHEAST, for instance, while indoors. We want to refer to the corner of the room, not to a wall (since most likely there will be two walls meeting in the northeast). Having taken care of that detail, we create a pair of regions, in order to put the backdrops in them.

A limitation of Inform, which may come into play if you try adapting the code in this example for use in your game, is that regions can’t overlap. (The basic way of handling region definitions is explained [here](../chapter_2_rooms_&_scenery/regions.md#regions).) Because of this limitation, if you use the code below you won’t be able to include both an indoor room and an outdoor room in any of the regions you might want to define in your game. Indoor rooms are in the Great Indoors region and outdoor rooms in the Great Outdoors region.

```inform7
A direction can be orthogonal or diagonal. A direction is usually orthogonal. Northwest is diagonal. Southwest is diagonal. Northeast is diagonal. Southeast is diagonal.

The Great Outdoors is a region. All outdoor rooms are in the Great Outdoors.
The Great Indoors is a region. All indoor rooms are in the Great Indoors.

The sky is in the Great Outdoors. The ground is in the Great Outdoors.

The floor is in the Great Indoors. The ceiling is in the Great Indoors. The east wall is in the Great Indoors. The north wall is in the Great Indoors. The west wall is in the Great Indoors. The south wall is in the Great Indoors.

The northeast corner is in the Great Indoors. The northwest corner is in the Great Indoors. The southeast corner is in the Great Indoors. The southwest corner is in the Great Indoors.
```

Next, we’ll add some code to let the player use commands of the form LOOK EAST. This type of command will do one thing if the player is in an indoor room (it will examine a wall) and another if the player is in an outdoor room (it will use the new direction-looking action that we’re about to define).

Note the use of the “listed instead of” line below to replace a default library rule with our own version. The library’s default just prints out a message, but we need more nuance.

```inform7
Carry out examining (this is the new examine directions rule):
      	if the noun is a direction:
            		if the location is an indoor room:
                  			repeat with item running through backdrops in the location:
                        				if the wall-direction of item is the noun:
                        					       try examining item instead;
            		otherwise:
                  			try direction-looking the noun instead;
      	otherwise:
            		continue the action.

The new examine directions rule is listed instead of the examine directions rule in the carry out examining rulebook.

Looking toward is an action applying to one visible thing. Understand "look toward [any room]" as looking toward.

Chosen direction is a direction that varies.

Check looking toward:
      	if the noun is the location:
            		try looking instead;
      	otherwise if the noun is not neighboring:
            		say "You can't see that far." instead.

Carry out looking toward:
      	now the chosen direction is the best route from the location to the noun;
      	try direction-looking the chosen direction instead.

Direction-looking is an action applying to one visible thing and requiring light. Understand "look [direction]" as direction-looking.

Carry out direction-looking:
      	let D be the noun;
      	if the location is an indoor room:
            		if D is inside or D is outside:
                  			say "You see nothing unusual.";
            		otherwise if D is up:
                  			try examining the ceiling instead;
            		otherwise if D is down:
                  			try examining the floor instead;
            		otherwise if D is diagonal:
                  			say "The [D] corner of the room is an ordinary corner.";
            		otherwise:
                  			say "The [D] wall looks like a wall.";
      	otherwise:
            		let R be the room D from the location;
            		if R is a room:
                  			assemble the huge-list for R;
            		otherwise:
                  			now the huge-list is {};
            		if the number of entries in huge-list is 0:
                  			say "You see nothing unusual in that direction.";
            		otherwise:			
                  			say "Looking [D], you can see [huge-list with indefinite articles]."
```

The code above uses a list (a global variable) called the huge-list, which we’ll create in the next section. The huge-list is not a permanent thing; we’ll assemble it dynamically each time it needs to be used. We’ll do this by checking for huge things. A huge thing, as you might imagine, is something that’s big enough to see from a distance when outdoors. Nothing in the game will be huge unless the author says it is.

Things that are huge will need to be added to scope in every turn when the player is in an outdoor room. This will assure that the player can refer to them in commands.

```inform7
A thing can be huge. A thing is usually not huge.

Definition: a room is neighboring if the number of moves from it to the location is 1.

After deciding the scope of the player when the location is an outdoor room:
      	assemble the huge-list;
      	repeat with item running through huge-list:
      		      place item in scope.

The huge-list is a list of things that varies. The huge-list is {}.

To assemble the huge-list:
      	now the huge-list is {};
      	let room-inv be a list of things;
      	repeat with R running through neighboring rooms:
            		now room-inv is {};
            		repeat with item running through things in R:
                  			add item to room-inv;
            		repeat with item running through room-inv:
                  			if item is huge:
                  				      add item to huge-list.

To assemble the huge-list for (R - a room):
      	now the huge-list is {};
      	let room-inv be a list of things;
      	repeat with item running through things in R:
            		add item to room-inv;
      	repeat with item running through room-inv:
            		if item is huge:
                  			add item to huge-list.

Instead of examining a huge thing:
      	if the noun is not in the location:
            		say "[The noun] [are] too far away for you to make out any detail.";
      	otherwise:
            		continue the action.

Before doing anything other than examining with a huge thing:
      	if the noun is not enclosed by the location:
            		say "[The noun] [are] too far away.";
            		rule fails;
      	otherwise:
            		continue the action.
```

Next, we’ll implement floorless rooms (more or less in the manner discussed [here](../chapter_2_rooms_&_scenery/floorless_rooms.md#floorless-rooms)). The reason for including floorless rooms in the example will become apparent in a moment.

```inform7
Limbo is a room. [Because this is the first room mentioned, we will soon have to make sure the player character starts the game in the Living Room.]

A room can be floorless. A room is usually not floorless. A room has a room called the drop zone. The drop zone of a room is usually Limbo.

After dropping something in a floorless room (called R):
        let DZ be the drop zone of R;
        move the noun to DZ;
        say "[The noun] plummets down out of sight."
```

The final facet of this example is to let the player throw things from one room into another (but only when outdoors). First we’ll add a few more vocabulary words as synonyms for “drop”. We really only want these words to be used in the new direction-throwing action, but if we don’t add them to the drop action, Inform will respond to the command TOSS THE BALL by saying “What do you want to toss the ball?” This would be ugly.

Note also that if there’s any reason in the game why the player won’t be allowed to drop things — such as being tied up — the game’s code will need to prevent direction-throwing in that circumstance as well. If you omit this step, the player will have an unintended way to drop things, by typing something like THROW RABID GERBIL EAST.

```ìnform7
Understand "hurl [something]", "toss [something]", and "pitch [something]" as dropping.

Understand "upward" as up.
Understand "downward" as down.
Understand "eastward" as east.
Understand "westward" as west.
Understand "northward" as north.
Understand "southward" as south.

Direction-throwing is an action applying to one thing and one visible thing and requiring light. Understand "throw [something] [direction]", "hurl [something] [direction]", "pitch [something] [direction]", and "toss [something] [direction]" as direction-throwing.

To bounce is a verb. [Here, we add some verbs so we can use them in brackets in the say statements in the rules we’re about to define. This will let Inform decide if the verb should be plural or singular in form.]

To come (he comes, they come, he came) is a verb.

[We're not going to let you throw things through a door from one room to another, on the theory that your aim isn't very good:]

Check direction-throwing:
        if the player does not carry the noun:
                say "You can't throw something you're not holding." instead;
        otherwise if the noun is huge:
                say "[The noun] [are] too heavy to throw." instead;
        otherwise if the location is not an outdoor room:
                say "[The noun] [bounce] off the wall and [come] to rest on the floor.";
                move the noun to the location;
                rule succeeds;
        otherwise:
                let D be the second noun;
                if the room D from the location is nowhere:
                        try dropping the noun instead.
```

If the direction-throwing action hasn’t been stopped by the check rule, we know (a) that the player is carrying the noun, (b) that the noun is small enough to throw, (c) that the player is outdoors, and (d) that there is a room in that direction, to which the noun can be thrown.

The carry out rule, below, moves the thrown object off into whatever room exists in the direction the player has thrown the object — unless the room in that direction is floorless. If the destination is floorless, the thrown object will instead end up in the drop zone of the floorless room.

The report rule checks to see where the noun has landed. If the player has tried to throw it up into a tree (a floorless room), it will by this time have landed somewhere else. This would most likely be the room the player is in (if she’s standing at the base of the tree) — but that’s not guaranteed. The player could be out on the limb of a tree and throw something south, toward the main part of the tree, thus causing it to drop to the ground below.

```inform7
Carry out direction-throwing:
      	let D be the second noun;
      	let R be the room D from the location;
      	if R is floorless:
            		let DZ be the drop zone of R;
            		now the noun is in DZ;
      	otherwise:
            		now the noun is in R.

To sail is a verb. To land is a verb.

To fall (he falls, they fall, he fell, it is fallen) is a verb.

Report direction-throwing:
        if the noun is in the location:
              	say "You throw [the noun], and [regarding the noun][they] [sail] away through the air, but a moment later [they] [fall] back and [land] beside you.";
        otherwise:
              	say "You hurl [the noun] [second noun], and [regarding the noun][they] [sail] away out of sight."
```

And here’s an entirely pointless scenario with a few rooms and objects, which you can use to test the example. You can try throwing things in various directions while indoors or outdoors, looking various directions while indoors and outdoors, and examining huge things that are far away.

```inform7
The Living Room is an indoor room. "The front door is north, the kitchen south."

The player is in the Living Room. The player carries some galoshes.

The Kitchen is south of the Living Room. The Kitchen is an indoor room. "Not much here. You can go north."

The Yard is an outdoor room. The yard is north of the Living Room. "The lawn wants cutting. The front door is south, and the hill is east."

The Hill is an outdoor room. The Hill is east of the Yard. "From the top of the hill, you can see back west into the yard. There's a tree here you could climb."

The buffalo is in the Hill. The buffalo is huge. The description of the buffalo is "Big and brown." [Absurdly, the buffalo can be picked up and carried around. This makes it easy to try throwing huge things and so forth.]

The cabbage is in the Hill.

The ferris wheel is in the Hill. The ferris wheel is huge. It is fixed in place. The description of the ferris wheel is "Big and round."

The Treetop is a floorless outdoor room. "You're surrounded by leaves." The Treetop is up from the Hill. The drop zone of the Treetop is the Hill.

The Treetop is a floorless outdoor room. "You're surrounded by leaves." The Treetop is up from the Hill. The drop zone of the Treetop is the Hill.
```

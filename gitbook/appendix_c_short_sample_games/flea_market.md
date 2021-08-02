## Flea Market {#flea-market}

We’ll start with a simple scenario that was suggested by Jay in a post on the newsgroup rec.arts.int-fiction, back in the day when it was still a go-to place for IF info. Jay’s goal was to make NPCs respond at random to items carried by the player. Each time the player takes inventory, one of the other shoppers in the flea market will notice some random thing the player carries, and comment on it.

This example illustrates four techniques: calling a function, creating a definition, using what computer programmers call a _switch_ statement, and using a while loop.

Inform’s switch statement (see **p. 11.8** of _Writing with Inform_, “Otherwise”)uses a double hyphen to indicate the various entries in the switch block. Only one of the lines in a switch block will be run at any given time. (A note to programmers: Inform doesn’t require break statements in switch statements.) In this case, we enter the switch block by selecting a random number between 1 and 5 and then choosing a say statement based on the value of the random number.

We’re creating a function (“To say the desire”) and passing it two arguments — a person and a thing. Within the function, we refer to the person as P and the thing as J. There’s nothing special about these symbols; we could just as easily have written “To say the desire of (dude - a person) for (stuff - a thing)” and then referred to “[dude]” and “[stuff]” in the say statements.

```inform7
To say the desire of (P - a person) for (J - a thing):
        if a random number from 1 to 5 is:
        -- 1: say "'Gee, I'd sure like to have a [J] like that,' [P] remarks.";
        -- 2: say "'That's sure a swell-looking [J],' says [P].";
        -- 3: say "[P] edges closer to you and says wistfully, 'I've been looking for years for a [J].'";
        -- 4: say "[P] hovers over you covetously. 'Say, were there more [J]s where you found that?'";
        -- 5: say "'Wow, that's a really nice [J],' [P] says enviously."

After taking inventory:
      	if nothing is held by the player or the player is alone:
            		rule succeeds;
      	otherwise:
            		let shopper be the player;
            		while shopper is the player:
                  			let shopper be a random person in the location;
            		let junk be a random thing held by the player;
            		say "[the desire of shopper for junk]".

Definition: a person (called P) is alone if the number of persons in the location of P is 1\.
```

The After rule causes nothing to happen if the player is alone or is carrying nothing. Before entering the while statement in the After rule, we define a variable called shopper, and give it the value of the player. When the while statement starts, shopper is the player. The while statement is a loop. It will execute over and over, randomly picking one person after another in the location, until the person it picks is _not_ the player. This is what we want; if the shopper is still the player, the output of the switch statement will be something like, “yourself edges closer to you and says wistfully....” Once the shopper is not yourself, the condition (while shopper is the player) becomes false, the loop ends, and the rest of the After rule runs. The rule chooses a random thing held by the player, combines it with the randomly chosen NPC, and says the desire of the random person for the random thing.

The definition is simple: We need to tell Inform what we mean by “alone,” because the “After taking inventory” rule needs to check this. Can you see what will happen if the “After taking inventory” rule doesn’t include the condition “if … the player is alone”? If the player ever takes inventory when no one else is in the location, the rule will go into an endless loop. The while statement will keep trying forever to find an NPC in the location, but it will always end up choosing the player.

Here’s the rest of the game:

```inform7
The Flea Market is a room. "All manner of things are for sale here, lined up in rows on folding tables."

A folding table is a supporter in the Flea Market. On the table are a replica Maltese Falcon, a phallic fertility statue of Aziz, a 1956 Ford carburetor, a headless Barbie doll, and a broken Pez dispenser.

Wanda is a woman in the Flea Market.
Julianne is a woman in the Flea Market.
Chrissie is a woman in the Flea Market.

The Parking Lot is north of the Flea Market. "Your car is parked here."

Test me with "i / take pez and ford and falcon and doll / i / i / i / i / n / i".
```

Since we don’t know what the player may be carrying or who may be in the location, we pretty much have to choose NPCs and held items at random. However, when items are selected at random, Inform will sometimes select the same item several times in a row. This can result in a repeating output, which will make the game seem wooden — but in a real game there might be only one NPC in the location, or the player might be carrying only one item, so repetition is not avoidable. If you’d prefer to minimize the repetition, you can at least step through the list of entries in the “To say the desire” rule in a repeating order, like this:

```inform7
The desire-index is a number that varies. The desire-index is 0.

To say the desire of (P - a person) for (J - a thing):
      	increase the desire-index by 1;
      	if the desire-index is greater than 5:
            		now the desire-index is 1;
      	if the desire-index is:
      	-- 1: say "'Gee, I'd sure like to have a [J] like that,' [P] remarks.";
      	-- 2: say "'That's sure a swell-looking [J],' says [P].";
      	-- 3: say "[P] edges closer to you and says wistfully, 'I've been
      looking for years for a [J].'";
      	-- 4: say "[P] hovers over you covetously. 'Say, were there more [J]s where you found that?'";
      	-- 5: say "'Wow, that's a really nice [J],' [P] says enviously."
```

Here, we’ve created a global variable (desire-index). It’s global so that it will persist throughout the game; a local variable within a rule will be destroyed when the rule finishes. We then increase the desire-index by 1 each time the rule runs and check to see if it has gone past 5\. If so, we reset it to 1\. Now the five statements will be used in the order shown, over and over (but with random people and random things).

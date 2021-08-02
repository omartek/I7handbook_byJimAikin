## Doing Calculations {#doing-calculations}

In a role-playing game (RPG), you may want to keep track of various characters’ strength and other characteristics. While the game is running, you may need to calculate things like their combat readiness based on various factors. The example below shows how this type of thing might be done. It uses Inform’s To Decide syntax to run calculations.

```inform7
A person has a number called strength. A person has a number called luck. A person has a number called dexterity.

To decide what number is combat-adds of (p - a person):
      	let num be a number; [this will default to 0]
      	let num be num + the modifier of the strength of p;
      	let num be num + the modifier of the luck of p;
      	let num be num + the modifier of the dexterity of p;
      	decide on num.

[Since the modifier formula is the same for each attribute, we can create a separate routine to calculate that and reuse it for each one. If the base value (strength, luck, or dexterity) is greater than 12, we’ll modify the combat-adds by adding the surplus to combat-adds. If it’s less than 9, we’ll subtract the difference from combat-adds:]

To decide what number is modifier of (n - a number):
      	let m be a number;
      	if n > 12, let m be n - 12;
      	if n < 9, let m be n - 9;
      	decide on m.

To say stats of (p - a person):
      	say "Strength: [strength of p]; Luck: [luck of p]; Dexterity: [dexterity of p].";
      	say "Combat Adds: [combat-adds of p]."

[Here's a generic dice-rolling routine:]
To decide what number is a (n - a number) d (m - a number) roll:
      	let tot be a number;
      	repeat with loop running from 1 to n:
            		let x be a random number between 1 and m;
            		let tot be tot + x;
      	decide on tot.

To char-roll (p - a person):
      	now the strength of p is a 3 d 6 roll;
      	now the luck of p is a 3 d 6 roll;
      	now the dexterity of p is a 3 d 6 roll.

[Purely for testing, the command JUMP will re-roll the player character:]
Instead of jumping:
      	say "Re-rolling your character...";
      	char-roll the player.

The Lab is a room.
When play begins:
      	char-roll the player;
      	say stats of the player.

Every turn: say stats of the player.

test me with "jump / g / g / g".
```

Several things about this example are worth study. In the “Instead of jumping” rule, for instance, we have “char-roll the player.” This calls the block of code just before it, “To char-roll (p – a person)”. This is Inform’s standard way of creating new functions. Once the “To char-roll” code is created, we could char-roll any character in the game. But the compiler won’t let us char-roll anything other than a person. The char-roll code needs to be sent a person object, because only persons have strength, luck, and dexterity.

In the odd-looking syntax, “now the strength of p is a 3 d 6 roll”, the dice-rolling routine rolls 3 dice that are 6-sided, adding the results to give a value somewhere between 3 and 18\. This value is computed in the “To decide what number is a … roll” code block.

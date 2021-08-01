## Smelling &amp; Listening {#smelling-listening}

Inform includes the commands “smell [something]” and “listen to [something]”, but they don’t do anything. The output is “You smell nothing unexpected” or “You hear nothing unexpected.”

An important part of writing good fiction (of any kind, not just interactive fiction) is letting your readers use all of their senses. Adding an odor or sound to a single object with an Instead rule is easy:

```inform7
Instead of smelling the garbage:
say "It smells awful!"
```

This will work if the player types SMELL GARBAGE. But the player might just type SMELL. As explained on **p. 7\. 7** of _Writing with Inform_, “The other four senses,” this command is redirected to smelling the location (the room) — and again, by default, the game replies, “You smell nothing unexpected.” If the garbage is in the location, this response is just plain wrong. If the garbage is fixed in place, we can give the room an Instead rule so that it will respond to the SMELL command:

```inform7
Instead of smelling the Alley:
say "It smells of garbage."
```

But we’ll have to do that for every room where there’s an odor, and if some of the things that have odors are getting moved around during the game, keeping track of them in order to list the odors will get messy.

Fortunately, it’s not hard to improve Inform’s handling of smelling and listening. The _Recipe Book_ provides several good examples of ways to add sounds to a game, so in the _Handbook_ we’ll concentrate on odors. In the code below, we’re going to give every thing in the game a scent (which is a text in quotes). By default, this text will be empty. But now we can add a scent as a property of a thing, rather than needing to write a whole new Instead rule. A single Instead rule (Instead of smelling something) will handle any object the player tries to SMELL.

The other feature we’ll add is this: We’ll define a thing as smelly if its scent is not “” (that is, when the scent property is not empty). When there is something smelly in the room, typing SMELL will list the smelly things in the room.

```inform7
A thing has some text called the scent.

Definition: A thing (called the odor-bearer) is smelly if the scent of the odor-bearer is not "".

Instead of smelling something:
if the noun is smelly:
say "[scent of the noun][paragraph break]";
otherwise if the noun is the player:
say "You don't smell too sweaty today.";
otherwise:
say "It smells like an ordinary [noun]."

Instead of smelling a room:
        let L be the list of smelly things enclosed by the location;
        if L is empty:
                say "You smell nothing unexpected.";
        otherwise:
                say "You smell [a list of smelly things enclosed by the location]."

The Kitchen is a room.
The banana is in the Kitchen. The scent of the banana is "It smells sweet and ripe."
The loaf of bread is in the Kitchen. The scent of the bread is "Ah -- fresh-baked bread."
```

Here’s the output when the player is in the Kitchen:

```
>smell
You smell a banana and a loaf of bread.
```

There are other ways to implement smelling. This is normal in writing interactive fiction — the author can usually solve the same problem by using several different techniques. Below is a simple example game that I’ve adapted from an example uploaded to the ifwiki (http://www.ifwiki.org/). It differs from the code shown above in a number of ways.

First, it implements the smelling action in a more complete way. Because it uses Carry Out and Report rules rather than Instead rules, it has to start by removing the block smelling rule from the Standard Rules. Second, it gives distinct odors to rooms rather than just listing any smelly objects that are in the room. Third, it has the beginnings of a puzzle, in the form of a spacesuit that will block smelling. Fourth, the odor of the sewage is so powerful that it will prevent you from smelling the flower.

```inform7
[First we'll create the property for all things and rooms.]
A thing has a text called odor.
A room has a text called odor.

Report an actor smelling (this is the new report smelling rule):
        if the actor is the player:
                if the action is not silent:
                        if the odor of the noun is not empty:
                                say "[the odor of the noun][paragraph break]";
                        otherwise:
                                say "[We] [smell] nothing unexpected." (A);
        otherwise:
                say "[The actor] [sniff]." (B).

The new report smelling rule is listed instead of the report smelling rule in the report smelling rulebook.

[The player might try 'smell the odor', so we'll allow that by creating a backdrop:]

The ambient-odor is a backdrop. It is everywhere. The description is "The odor is impalpable." Understand "odor", "odour", "stench", "stink", "fragrance", "reek", and "smell" as the ambient-odor.

Instead of doing anything other than smelling or examining with the ambient-odor:
        try examining the ambient-odor.

Instead of smelling the ambient-odor:
        try smelling the location.

Street is a room. "You are in a street. The sewer is below you." The odor is "You pick up a faint odor from below."
A flower is here. The description is "It's just a nice flower. You don't know what type." The odor is "It smells wonderful."
A spacesuit is here. It is wearable. Understand "space suit" and "suit" as the spacesuit. The description is "Spacesuits are wonderful things, but they make EVERYONE look fat."

Sewer is below Street. "You are in a sewer. The street is above you."
Some sewage is here. It is fixed in place. The description is "Horrible smelly sewage is everywhere in the sewer." The odor is "It reeks."

[Finally we'll add some rules to restrict smelling.]
Instead of smelling when the spacesuit is worn and the noun is not yourself and the noun is not the spacesuit:
        say "You can't smell anything outside the spacesuit while wearing the spacesuit."
Instead of smelling in the presence of the sewage when the spacesuit is not worn and the noun is not the sewage:
        say "The disgusting reek of the sewage overwhelms your nose. You can't smell anything else."
```

In passing, you might want to take note of the lists of conditions in those last two Instead rules. This syntax is not used much in the _Handbook,_ but it’s good to know about it.

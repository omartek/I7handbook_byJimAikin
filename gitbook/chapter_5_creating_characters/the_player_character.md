## The Player Character

Pleasantly little needs to be said about creating the player character (PC). Your PC can have any identity you might like, from a mile-high evil robot to a small, cuddly bunny rabbit. Or the PC could be a sort of blank — a shadow character that the actual player can project his or her own personality into.

To start creating a PC, all you need to do is write a description:

```inform7
The description of the player is "In the absence of a mirror, you're not quite sure what you look like today."
```

In games that are puzzle-oriented rather than people-oriented, that may be all you need to do. Depending on the character you’ve chosen, though, you may want to write non-standard messages for situations in which the PC either does something, or doesn’t. For instance, your PC might be very timid. In that case, the PC would naturally hesitate to do certain things that another PC might have no trouble doing:

```inform7
Instead of taking the spider, say "You can't bring yourself even to get near it."
```

At the other extreme, the PC might be rambunctious, ill-mannered, or just plain evil. He might enjoy breaking things, for instance. This fact could lead you to write code like this:

```inform7
Some dishes are in the Lab. The dishes can be broken or unbroken. The dishes are unbroken. The printed name of the dishes is "[if broken]broken [end if]dishes". Understand "broken" as the dishes when the dishes are broken.

Instead of attacking the dishes:
        if the dishes are broken:
                say "You already took care of that little chore.";
        otherwise:
                now the dishes are broken;
                say "You smash the dishes with gusto!"
```

The point of this code is to respond to the command BREAK THE DISHES with the line, “You smash the dishes with gusto!” Customizing Inform’s standard outputs is a simple way of giving a specific character to the PC.

In the early days of interactive fiction, a number of games were released in which the PC changed identity during the course of the game — essentially, switching from one body to another. This isn’t done too often anymore, but if you want to do it, it isn’t difficult. All you need is a couple of lines of code. In the silly little example below, we’ll use pressing a button to cause the PC to swap bodies with an NPC. In a real game, you might use a magical device of some sort, or have the PC wake up from a dream and discover that she’s really someone else.

```inform7
The Test Lab is a room. "Many devious tests are conducted here."

Bingo is an animal in the Lab. The description is "[if the player is Bingo]You are[otherwise]Bingo is[end if] a peppy-looking cocker spaniel."

Bob is a man in the Lab. The description is "[if the player is Bob]You are[otherwise]Bob is[end if] a heavyset, muscular man."

The player is Bob.

Linda is a woman in the Lab. The description is "[if the player is Linda]You are[otherwise]Linda is[end if] a sultry and curvaceous beauty."

The red button is in the Lab.

Instead of pushing the red button:
        if the pla        yer is Bob:
                now the player is Linda;
                say "A strange tingly feeling overtakes you. You feel much more feminine than before.";
        otherwise if the player is Linda:
                now the player is Bingo;
                say "Your head spins. When you recover, things seem to have changed. The world is larger, and you're covered with fur.";
        otherwise:
                now the player is Bob;
                say "You feel odd for a moment Yes, you're human again, and muscular, and male."
```

In a real game, many other messages and rules would have to test whether the player is Bob, Linda, or Bingo, and change the results of the player’s commands based on the PC’s identity.

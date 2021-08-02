## Hidden Items

Experienced players of IF know to EXAMINE everything that’s mentioned in the room description, or in a description of another object. So it’s fair to tuck clues to various puzzles in descriptions. Quite often, the room will contain an object which is itself scenery, but which will reveal further details when examined. The description of a wall panel, for instance, might suggest to the player that the panel is a secret door. Or maybe the panel looks entirely innocent when examined, but if the player examines the rug he’ll learn that a semicircular mark on the rug curves out from the wall panel. (If you’re going to do that, be sure to mention the rug in the room description.) The details are “hidden” only in a technical sense, because you have to examine something else in order to notice them, so this is only barely a puzzle. Many games that award points don’t award any points for examining things, because the action is just too easy and obvious.

Examining won’t always reveal hidden items, however. As a player, you’ll want to get in the habit of looking under and behind anything large. Containers may need to be searched in order to reveal what’s hidden in them. By default, Inform will list the contents of any open container when the player examines the container, but as an author you might want to make the puzzle a tiny bit more difficult. If you do this, though, it would be a courtesy to the player to provide a clue that more action needs to be taken. Here’s a not very subtle example, in which “almost anything might be buried down there” serves as a clue:

```inform7
The Living Room is a room. "Your comfy living room."

The big old box is an open container in the living room.The description is "It's just a big old box[one of] full of junk. There's so much stuff that almost anything might be buried down there[or][stopping]."

The pile of old junk is in the box. The description is "A horrible mass of rusty old junk." Understand "rusty" as the junk.

Instead of taking the junk:
        say "You have no need to burden yourself with a pile of old junk."

The jewel-encrusted bracelet is a thing. The description is "Diamonds and sapphires and rubies, oh my!"

Instead of searching the box for the first time:
        try searching the junk.

Instead of searching the junk for the first time:
        say "Down among the rusty junk, you spot a priceless jewel-encrusted bracelet!";

now the bracelet is in the box.
```

The result, when the game is played, looks like this:

```
Living Room

Your comfy living room.

You can see a big old box (in which is a pile of old junk) here.

>x box
It's just a big old box full of junk. There's so much stuff that almost anything might be buried down there.

In the big old box is a pile of old junk.

>look in box
Down among the rusty junk, you spot a priceless jewel-encrusted bracelet!

>x box
It's just a big old box.

In the big old box are a jewel-encrusted bracelet and a pile of old junk.
```

The LOOK IN command causes the same action as SEARCH.

A sorting puzzle probably qualifies as a subtype of the hidden item puzzle. In a sorting puzzle, there are a great many similar or seemingly identical objects, all available at the same time. Your goal is to find a way to distinguish the one you want from all of the others. For an especially fiendish example of this, you might want to download and play the game “69,105 Keys.” It’s a one-room game with a locked vault, and, you guessed it, 69,105 keys, only one of which opens the vault.

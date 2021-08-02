## Changing the Map During the Game

In most of the games you may write, the model world will work the way you want it to if you create connections between rooms at the beginning of the game (that is, when creating the rooms in your source) and then leave the connections alone. But once in a while, you may want a connection between rooms to disappear while the game is being played — maybe because the rooms are in a cave complex and there has been a cave-in blocking a tunnel. Or maybe a magic door has suddenly appeared in a room, creating a connection where there wasn’t one before. The magic door might even have a mind of its own, and wander off again. (Inform doesn’t allow doors to be moved around during the game; if you want a magic door to move around, you’ll have to write some extra code to create an ordinary object that responds to the player’s commands as if it were a door.)

To get rid of an exit from a room, change that direction of the room to nowhere. (It’s usually a good idea to do this to both sides of the connection between rooms, just in case there’s another route the player can use to get around to the other side of the blocked exit.) To restore an exit or create a new one, change the exit so that it points to the room that is the destination.

Here’s a simple test game that shows how to do it. In this game, if the player tries the command UP before the Tree House has been visited, the only result will be a nudge (“You gaze speculatively....”) Once the tree has been climbed, however, the UP command will work.

```inform7
The Forest Path is a room. "Tall old trees surround you. That old oak tree, for instance."

The Tree House is a room. "What an amazing view!"

The old oak tree is scenery in the Forest Path. The description is "It's a sturdy old tree."

Instead of going up in the Forest Path:
        if the Tree House is unvisited:
                say "You gaze speculatively at the old oak tree. It looks as if it might be climbable.";
        otherwise:
                continue the action.

Instead of climbing the old oak tree:
        change the up exit of the Forest Path to the Tree House;
        change the down exit of the Tree House to the Forest Path;
        say "You clamber up the tree....";
        now the player is in the Tree House.
```

Next we’ll look at a somewhat artificial example that has one or two added features. In this short game there are two north-south connections (between the Living Room and the Kitchen, and between the Bathroom and the Bedroom), but only one of them will exist at any time, depending on which button you push. To make the changes easier to test, I’ve put the buttons on a backdrop, so that they’re always present no matter what room you’re in. I also included Exit Lister, which will display the current exits in the status line. Notice that the status line will be updated each time you press a button.

```inform7
Include Exit Lister by Eric Eve.

The Living Room is a room. "You can definitely go east here. You may or may not be able to go south."

The Kitchen is south of the Living Room. "You can definitely go east here. You may or may not be able to go north."

The Bedroom is east of the Living Room. "You can definitely go west here. You may or may not be able to go south."

The Bathroom is east of the Kitchen. "You can definitely go west here. You may or may not be able to go north."

The floating button holder is a backdrop. It is everywhere. It is not scenery.

Does the player mean pushing the floating button holder: It is very unlikely.

Rule for writing a paragraph about the floating button holder:

say "A button holder is floating in mid-air here. On it are a red button and a green button."

The red button is part of the floating button holder. The green button is part of the floating button holder.

Instead of pushing the red button:
        change the south exit of the Living Room to nowhere;
        change the north exit of the Kitchen to nowhere;
        change the south exit of the Bedroom to the Bathroom;
        change the north exit of the Bathroom to the Bedroom;
        say "Living Room south is gone, Bedroom south is open."

Instead of pushing the green button:
        change the south exit of the Living Room to the Kitchen;
        change the north exit of the Kitchen to the Living Room;
        change the south exit of the Bedroom to nowhere;
        change the north exit of the Bathroom to nowhere;
        say "Living Room south is open, Bedroom south is gone."
```

This neat little trick won’t work with doors, unfortunately. Inform has rigid ideas about how doors work. It’s possible to make a door seem to disappear during the game, even though it’s still present. Doing this is awkward and error-prone, but the place to start would be with the Secret Doors extension, which is discussed earlier in this chapter. A better approach might be, as mentioned earlier, to create an ordinary thing that responds to the user’s commands as if it were a door.

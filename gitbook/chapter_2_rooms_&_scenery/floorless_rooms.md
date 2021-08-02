## Floorless Rooms

As mentioned at the beginning of this chapter, when the player uses the DROP command to get rid of objects that are being carried, the convention of IF is that the objects end up on the floor. This is usually a sensible way for objects to behave — but what if the “room” is the top of a tree?

Creating a floorless room turns out to be very easy:

```inform7
A floorless room is a kind of room. A floorless room has a room called the drop-location.

The Forest Path is a room. "Tall old trees surround you. That magnificent oak, for instance."

The old oak tree is scenery in Forest Path. "Plenty of low-hanging branches. You could probably climb it."

Instead of climbing the old oak tree:
        try going up.

Top of the Oak Tree is up from the Forest Path. "The view from here is inspiring!" Top of the Oak Tree is a floorless room. The drop-location of Top of the Oak Tree is Forest Path.

After dropping something in a floorless room (called F):
        move the noun to the drop-location of F;
        say "[The noun] drop[s] out of sight."

The only thing you need to be careful of, with this code, is that every floorless room _must_ have its drop-location defined. If you forget to do this, things that are dropped will end up (oddly enough) in the starting location of the game — the first room defined in your source.

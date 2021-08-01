## Initial Appearance {#initial-appearance}

When you create a new object and put it in a room, it will be mentioned right after the room description, but in a very basic way. If we’ve created a banjo, for instance, the room description will end with a paragraph that reads, “You can see a banjo here.”

Inform objects have a special property called **initial appearance**. If an object has an initial appearance, this will be used in the room description until the object has been picked up by the player.

If Inform sees a quoted sentence just after a new object has been created, it will know that this is the initial appearance of the object. We could create our banjo like this:

```inform7
The Meadow is a room. "Wildflowers carpet the meadow."

The old banjo is in the Meadow. "A banjo lies forgotten among the wildflowers." The description is "It&#039;s a 1938 Selmer 5-string."
```

The sentence “A banjo lies forgotten among the wildflowers” is the initial appearance of the banjo. The term “initial appearance” is actually the name of a **property** that objects can have in Inform. Properties are a type of data that’s attached to an object. The description of an object is another of its properties, and the printed name (shown earlier in the example that involved leprechauns) is yet another.

When we give the banjo an initial appearance, this is what will happen when the player enters the Meadow:

```
Meadow
Wildflowers carpet the meadow.
A banjo lies forgotten among the wildflowers.
```
Having the line about the banjo off in a paragraph by itself looks a little odd, but that’s mainly because the room description of the meadow is so brief. If the room description were three lines long, having a new paragraph about the banjo would look perfectly natural.

An initial appearance will be used only until an object is picked up for the first time by the player character. There may be times when you’d like an object to be referred to in a non-default way in room descriptions on an ongoing basis, or possibly in several non-default ways depending on which room it’s in. The following code does that:

```inform7
Rule for writing a paragraph about the shovel: say "[if the shovel is in the Garage]Your shovel lies in the corner against the wall.[otherwise if the shovel is in the Tool Shed]On a shelf is your handy shovel.[otherwise if the shovel is in the Work Site]Your shovel is stuck in the ground here.[otherwise]You seem to have left the shovel lying here.[end if]".
```

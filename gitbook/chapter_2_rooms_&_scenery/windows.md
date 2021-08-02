## Windows {#windows}

Real rooms often have windows. Windows have some interesting features. When you look through a window, you’ll normally see what’s on the other side. If the window is open, you may also be able to climb through it. (Or not.) A window is normally in two rooms, like a door. And if the room on one side of a window is lighted, it’s very unlikely that the room on the other side will be a dark room. (For more on dark rooms, [here](../chapter_2_rooms_&_scenery/dark_rooms.md#dark-rooms))

The easiest way to make a window that the player can actually climb through is to make it a door. This will handle the player’s travel automatically, and will also keep the two sides of the window “in sync” with respect to whether they’re open or closed. Since Inform doesn’t understand “climb through”, we’ll also create a new action to let the player use the window:

```inform7
The Lab is a room. "Welcome to the Test Lab. Many devious tests are conducted here. There's a wide window in the north wall."

The Porch is a room. "There's a wide window in the south wall."

The wide window is a door. The wide window is scenery. The wide window is north of the Lab and south of the Porch.

Climbing through is an action applying to one thing. Understand "climb through [something]", "climb in [something]", "climb out [something]", and "climb out of [something]" as climbing through.

Check climbing through:
        if the noun is not a door:
                say "You can't climb through [a noun]!" instead;
        otherwise:
                try entering the noun instead.
```

The commands LOOK THROUGH WINDOW and LOOK IN WINDOW cause Inform to run the SEARCH action. However, LOOK OUT WINDOW and LOOK OUT OF WINDOW aren’t understood. We can use an Instead rule to write a description of whatever is on the far side of the window, and add an Understand directive that will give the player two more ways to look through the window.

```inform7
Instead of searching the wide window:
if the location is the Porch:
                say "There seems to be a laboratory in there, but you can't make out any details.";
        otherwise:
                say "Through the window you can see the porch, but the view isn't good enough for you to make out any details."

Understand "look out of [something]" and "look out [something]" as searching.
```

If we wanted to mention any large objects that would naturally be visible through the window, such as a rocket on a launching pad, we can create them as distant scenery, using the techniques shown earlier in this chapter. Another refinement, which you may want to try working out for yourself, would be to make the “look out of” action different from the “look in” action, so that the player can look out the window only when in an interior-type location, and can look in the window only when in an exterior-type location. Depending on how your rooms are laid out, this might be accomplished using Regions (see [here](../chapter_2_rooms_&_scenery/regions.md#regions)).

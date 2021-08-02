## Enterable Containers &amp; Supporters

Some containers and supporters might be big enough that the player could reasonably enter them — a chair or bed, for instance. Here is a simple example that includes both:

```inform7
The Bedroom is a room. "Your basic bedroom. It's equipped with a bed and a chair."

The bed is an enterable scenery supporter in the Bedroom. The chair is an open enterable scenery container in the Bedroom.
```

The player will get able to GET IN BED or SIT ON BED, but not LIE IN BED or LIE DOWN IN BED, because the action “lie in” has not been defined. If you aren’t sure how to make a new action, turn to Chapter 4 of the _Handbook,_ “Actions.” The standard command used by the player to get out of an enterable container is STAND (or STAND UP, or EXIT). Annoyingly, GET OUT OF BED is not recognized by the parser. In order to handle this command, we need to write a little extra code:

```inform7
Getting out of is an action applying to one thing. Understand "get out of [something]" as getting out of.

Carry out getting out of something:
        try exiting instead.
```

When an openable container is enterable, the player will be allowed to close it from the inside. Inform understands that the inside of a closed container is dark, so if the player enters the container and then closes it, the player will be in darkness — unless carrying a light source, of course.

```inform7
The refrigerator is an openable enterable container in the Kitchen. The description is "An old white General Electric fridge." Understand "fridge" as the refrigerator. The refrigerator is open.
```

By default, the player will be allowed to pick up things that are in the room (that is, on the floor) even when in or on an enterable container or supporter. This is not too realistic, so you might want to prevent it. I’m a little nervous about the syntax of the next bit of code, because at any given moment either C or S will be nothing ... but it seems to work:

```inform7
Before taking something:
        if the player is enclosed by an enterable container (called C) or the player is enclosed by an enterable supporter (called S):
                if the noun is not enclosed by C and the noun is not enclosed by S:
                        say "You can't reach [the noun] from here." instead.
```

The syntax shown above, in which we use the phrases “(called C)” and “(called S)” to create temporary local values for things so that we can test them, is one that you’ll use a lot in writing if-tests in Inform.

If the player is on an enterable supporter or in an enterable container, trying to go somewhere will cause the parser to print out the message “You would have to get off [the supporter] first.” This is realistic, but a bit annoying, since the player knew what she wanted to do. Here’s an easy way to fix it, suggested by Michael Callaghan:

```inform7
Instead of going when the player is on a supporter (called S):
        say "(First getting off the [printed name of S])[command clarification break]";
        surreptitiously move the player to the holder of S;
        continue the action.

Instead of going when the player is in a container (called C):
        say "(First getting out of the [printed name of C])[command clarification break]";
        surreptitiously move the player to the holder of C;
        continue the action.

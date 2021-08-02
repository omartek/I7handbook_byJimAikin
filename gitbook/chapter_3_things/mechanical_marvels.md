## Mechanical Marvels

Inform provides a kind of thing called a device. The idea is, if you want to create something that can be switched on or off, you can call it a device. Inform will then understand that the commands SWITCH ON and SWITCH OFF can be applied to it (along with a few synonyms, such as TURN ON and TURN OFF). A device keeps track of whether it’s switched on or switched off, so this property can be tested in your code:

```inform7
if the electric razor is switched on:
        now the player is clean-shaven;
        [...and so on...]
```

The only other thing a device does, by default, is this: If the player examines it, the game will report whether it’s currently switched on or switched off. That’s okay if the device is something like an electric fan, which has a large black plastic on/off switch with the words ON and OFF printed on its mounting. It’s less desirable if the device has no visible switch and doesn’t look any different when it’s switched on. In that case, we might prefer to prevent Inform’s automatic mention of the device’s on/off state. This can be done by removing the rule that causes the state to print out, like this:

```inform7
The examine devices rule is not listed in any rulebook.
```

If you do this, it’s up to you to write a description for each device that will alert the player to the device’s state:

```inform7
The description of the electric razor is "It's a Remington cordless[if switched on]. At the moment it's humming faintly[end if]."
```

If you want the on/off state to not be mentioned with respect to only one device, unlisting the examine devices rule is like unscrewing a screw with a shovel. Instead, do this:

```inform7
The examine devices rule does nothing when the noun is the electric razor.
```

(Note: This procedure only works from 6L02 onward; if you’re using an older version of Inform, you’re on your own.) Another odd thing about Inform’s default implementation of devices — well, let’s stick with the electric razor for a minute. The command SWITCH RAZOR means the same thing as SWITCH RAZOR ON. I personally prefer to have the command SWITCH RAZOR operate as a toggle: Giving the command when the razor is off should turn it on, and giving the command when the razor is on should turn it off. I managed to figure out one way to do this, and then Emily Short suggested a better way. In the interest of providing a more complete tutorial, let’s look at them both.

My method requires a side trip to **p. 17.3** of _Writing With Inform_ (“Overriding existing commands”), where you’ll learn how to detach the word “switch” from the switching on action.

```inform7
Understand the command "switch" as something new.
```

The tricky thing is, when we do this, SWITCH ON and SWITCH OFF won’t work either, because we’ve detached the word “switch” from _all_ commands. So in addition to creating a new action (which we’ll call toggling), we also have to replace the grammar for SWITCH that we want to work the way it did before.

Here’s the final version of my code:

```inform7
Understand the command "switch" as something new.
Understand "switch [something] on" and "switch on [something]" as switching on.
Understand "switch [something] off" and "switch off [something]" as switching off.

Toggling is an action applying to one thing and requiring light. Understand "toggle [something]" and "switch [something]" as toggling.

Check toggling:
        if the noun is not a device:
                say "[The noun] can't be toggled on and off."

Carry out toggling:
        if the noun is switched on:
                try switching off the noun instead;
        otherwise:
                try switching on the noun instead.
```

Now the command SWITCH RAZOR will alternately switch the razor on and off.

Emily’s method is much simpler, and illustrates a cool feature of Inform programming:

```inform7
Understand "switch [a switched on thing]" as switching off.
```

That’s it — that’s the whole answer. Emily explains it this way: “Because ‘a switched on thing’ is more specific than ‘a thing’, this understand line will be sorted early in the parse list and will be matched first if it applies [to the player’s input]. Switched off things will continue to be caught by the existing understand line. The clever use of adjectives in understand tokens is a useful technique to have in one’s Inform programming repertoire. It’s possible to tuck some complicated logic into the parser without having to write a separate action for each possible variation.”

The default response when a device is switched on or off is this:

```
>switch on razor
You switch the electric razor on.
```

This is functional, but with some devices, we might want something more descriptive. If you simply write a “Report switching on” rule for your device, it will run — and then the standard report switching on rule in the library will run, resulting in a double output:

```
>switch on razor
The razor begins humming faintly.

You switch the electric razor on.
```

This is obviously undesirable. Here’s how to get rid of it for a specific device:

```inform7
Report an actor switching on (this is the new report switching on rule):
        if the action is not silent:
                if the noun is the razor:
                        say "The razor begins humming faintly.";
        otherwise:
                say "[The actor] [switch] [the noun] on." (A).

The new report switching on rule is listed instead of the standard report switching on rule in the report switching on rulebook.
```

With this code in place, your own report for the action of switching on the razor will be the only output displayed in response to the action.

Creating buttons that can be pushed and levers that can be pulled is almost too simple to be worth mentioning:

```inform7
The silver lever is a part of the shiny blinking plastic box.

Instead of pulling the silver lever:
        say "Clunk! You pull the lever, and a silver dollar drops into the hopper.";
        let SD be a random silver dollar in the money bin;
        now SD is in the hopper.
```

Example 298 in the Documentation, “Safety,” shows how to make a spinning dial on a safe, but the example is hardly complete. For one thing, the dial doesn’t exist as a separate object that can be examined. And because it can’t be examined, there’s no way to find out what number it’s currently set to. A question on the newsgroup rec.arts.int-fiction (back when it was still used as a forum for IF discussion, before intfiction.org became the central hub) included some code for a dial that could be set to any number from 1 to 8. I modified the posted code slightly and came up with this dial:

```inform7
The rotary dial is part of the safe. The dial has a number called current setting. The current setting of the dial is 1. The dial has a number called max setting. The max setting of the dial is 8. The description of the dial is "The rotary dial has eight numbers, 1 through [max setting]. At the moment it's set to [current setting]."

Instead of turning the dial:
        increase the current setting of the dial by 1;
        if the current setting of the dial > max setting of the dial:
                now the current setting of the dial is 1;
        say "You turn the dial to [current setting of the dial]."

Understand "set [something] to [number]" as setting the state of it to. Setting the state of it to is an action applying to one thing and one number. Understand "turn [something] to [number]" or "turn [something] to setting [number]" or "turn [something] to position [number]" or "adjust [something] to [number]" or "adjust [something] to position [number]" or "adjust [something] to setting [number]" as setting the state of it to.

Check setting the state of it to:
        if the noun is not the rotary dial:
                say "You can't set [the noun] to a number." instead;
        if the number understood &lt; 1, say "The lowest setting is 1." instead;
        if the number understood &gt; max setting of the dial, say "Sorry, the dial can only be set from 1 to [max setting of the dial]." instead.

Carry out setting the state of it to:
        now the current setting of the noun is the number understood;
        say "You turn the dial to [number understood]."
```

Combining this code with Example 298 would require a little more work. In a real game, you might want to create three dials of this type, and mount them side by side on the door of the safe. This would force the player to figure out what three-digit number to dial. You might also want to write some code that would interpret DIAL 123 as a command to set the first dial to 1, the second dial to 2, and so on. I’ll leave this as an exercise for you to try on your own. The main things to notice about the code given above are:

1.  A new action, setting the state of it to, can be used to SET DIAL TO 3 (or any other number between 1 and the max setting of the dial).

2.  The command TURN DIAL will increment (add 1 to) the setting of the dial.

3.  If the dial is already at its max setting, TURN DIAL will rotate it around to 1 again.

Many other kinds of mechanical contrivances might be useful in your game. If you want to create a tricycle that the player can ride, for instance, you’ll want to look at the extension called Rideable Vehicles by Graham Nelson, which is now built into Inform. In Appendix C of this _Handbook,_ you’ll find an example of a device (the “Omega Machine”) that will respond to commands.

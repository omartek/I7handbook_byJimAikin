## Replacing Rules in the Standard Library

If you open up the extension called the Standard Rules, you’ll find the guts of Inform 7\. Or at least, the higher-level guts; there’s a lower level, as explained at the end of this Chapter, in the section “What does Inform 6 Have to Do with Inform 7?” The Standard Rules are not exactly light reading, but you can start to get a better idea of what’s going on in Inform by skimming them. You’ll find, for instance, this bit of code:

```inform7
Check an actor taking (this is the can't take scenery rule):
        if the noun is scenery:
                if the actor is the player:
                        say "[regarding the noun][They're] hardly portable." (A);
                stop the action.
```

This is the rule that produces the output “That’s hardly portable” if the player tries to take something that’s scenery. But let’s say you don’t care for this message. The way to make such changes is _not_ to edit the Standard Rules file. You can edit this file if you feel compelled to, but you’re inviting disaster. Inform provides a more elegant solution. The rule above, like most of the rules in the Standard Library, has a name. It’s called the can’t take scenery rule. If you want to replace this rule, perhaps to produce a message that you like better, here’s how to do it:

```inform7
Check an actor taking (this is the new can't take scenery rule):
        if the noun is scenery:
                if the actor is the player:
                        say "[regarding the noun][They're] not even faintly portable." (A);
                stop the action.

The new can't take scenery rule is listed instead of the can't take scenery rule in the check taking rulebook.
```

If you only want to change the message for one particular scenery object (or for a kind of scenery object), you can do it even more easily:

```inform7
Check an actor taking the boulder:
        say "You'd give yourself a hernia.";
        stop the action.
```

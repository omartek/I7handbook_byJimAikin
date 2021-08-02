## More about Collections &amp; Kinds

Inform lets you make either unique objects or kinds of objects. One reason to make several objects of a given kind is because they’re indistinguishable from one another, like the pennies in the section “Plurals &amp; Collective Objects,” above. But sometimes we want to make several objects of a single kind that are similar, yet different — for example, the various kinds of fruit in the section “Things vs. Kinds,” which starts [here](../chapter_3_things/things_vs_kinds.md#things-vs-kinds). When we do this, the player may very reasonably want to perform an action on all of the members of the kind at once (or at least, on all of the members that are available at that point in the game). Persuading Inform to report the action in a graceful way is not guaranteed to be simple.

The extension Consolidated Multiple Actions, as mentioned earlier, can handle some of these situations, but not all of them. If you want this extension to be used with any new actions you define in your game, you’ll need to write a bit of extra code. This rather gross example shows how to do it:

```inform7
Include Consolidated Multiple Actions by John Clemens.

The Test Lab is a room.

Moe is a man in the Lab.

A glop is a kind of thing. The indefinite article of a glop is "some". Understand "glop" as a glop. Understand "glop" as the plural of glop.

The jelly is a glop. The glue is a glop. The taco sauce is a glop. The player carries the jelly, the glue, and the taco sauce.

Smearing it on is an action applying to two things and requiring light. Understand "smear [things] on [something]" as smearing it on.

Report smearing it on:
        say "You smear [the noun] on [the second noun]."

Last for reporting consolidated actions rule when smearing on:
        say "You smear [consolidated objects] on [the second noun]."
```

The output looks like this:

```
>smear glop on moe
You smear the jelly, the glue and the taco sauce on Moe.
```

Consolidated Multiple Actions produces the output line — but in order for it to do its work, you have to do two things. First, your new action (in this example, the new action is called smearing it on) has to be defined using the “[things]” token, so that it can be used with multiple objects. Second, the action needs a “for reporting consolidated actions rule”. Oddly enough, this rule has to be written for the action “smearing on” rather than the action “smearing it on” — don’t ask me why.

The third aspect of this example, creating a kind called glop, is only a nice extra. Even if we hadn’t done this, Consolidated Multiple Actions could handle a list of objects, like this:

```
>smear jelly and glue on moe
You smear the jelly and the glue on Moe.
```

There are also times when we would like the player to be able to examine a group of related objects (such as several objects of the same kind) and read a single result. The examining action can’t normally be used by the player to look at more than one object at a time, so the default response if you try to examine several things is, “You can’t use multiple objects with that verb.” The method described in the old edition of the _Handbook_ for examining multiple objects no longer works, because of improvements in the Inform parser. However, a new and better way to get the same output is described in Example 295, “The Left Hand of Autumn.” This example shows how to set up a multiply-examining action that can handle several different lists of items, so let’s see if we can simplify it a bit. The tricky part (if you’re new to the rather twisty business of how Inform handles commands, which we’ll get into in Chapter 4) is making sure the command processing sequence does what we want it to, and then stops. This is the purpose of the truth state called group-description-complete in the following code.

```inform7
The Guardhouse is a room.

A guard is a kind of person. Understand "guard" and "man" as a guard. Understand "men" as the plural of a guard. The description of a guard is usually "He's wearing armor and a tarnished tin nametag that says '[the noun].'"

Moe is a guard in the Guardhouse. Larry is a guard in the Guardhouse. Curly is a guard in the Guardhouse.

Guard list is a list of objects which varies. Guard list is { Curly, Larry, Moe }.

When play begins:
        sort guard list.

Understand "examine [things]" or "look at [things]" as multiply-examining. Multiply-examining is an action applying to one thing.

Understand "examine [things inside] in/on [something]" or "look at [things inside] in/on [something]" as multiply-examining it from. Multiply-examining it from is an action applying to two things.

Group-description-complete is a truth state that varies.

Carry out multiply-examining it from:
        try multiply-examining the noun instead.

Check multiply-examining when group-description-complete is true:
        stop the action.

Carry out multiply-examining:
        let L be the list of matched things;
        if the number of entries in L is 0, try examining the noun instead;
        if the number of entries in L is 1, try examining entry 1 of L instead;
        describe L;
        say line break;
        now group-description-complete is true.

Before reading a command:
        now group-description-complete is false.

The silently announce items from multiple object lists rule is listed instead of the announce items from multiple object lists rule in the action-processing rules.

This is the silently announce items from multiple object lists rule:
        unless multiply-examining or multiply-examining something from something:
                if the current item from the multiple object list is not nothing, say "[current item from the multiple object list]: [run paragraph on]".

Definition: a thing is matched if it is listed in the multiple object list.

To describe (L - a list of objects):
        sort L;
        if L is guard list:
                say "They're wearing armor and nametags, which identify them as Moe, Larry, and Curly.";
        otherwise:
                say "You see [L with indefinite articles]."
```

For a simple example that shows how to consolidate the output messages when a collection of objects can get into different states, see “Broken Eggs” Appendix C.

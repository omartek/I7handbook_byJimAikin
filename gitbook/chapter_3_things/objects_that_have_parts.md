## Objects That Have Parts

In real life, most objects are made up of various parts. For instance, an electric stove has heating elements (burners), perhaps an oven built into it, and knobs for turning the burners on and off. Inform lets us model a complex object like a stove by defining the other objects that are its parts.

With simple objects such as a knife or a cup, there’s usually no need to create separate objects to model the parts. We can just make the names of the parts refer back to the main object, like this:

```inform7
The player carries a knife. The description is "It’s a shiny Bowie knife with a sharp three-inch blade and a black leather hilt." Understand "shiny", "Bowie", "sharp", "blade", "black", "leather", and "hilt" as the knife.
```

If the player types X BLADE or X HILT, the game will simply print out the description of the knife. That may be all that we need. But with a more complex object, adding parts is a good way of designing it. The basics of how to do this are well explained on **p. 3.23** of _Writing With Inform_ (“Parts of things”). Example 36 (“Brown”), on that same page, shows how to make parts that can be detached and reattached. Unless our code detaches a part of an object, it will always be part of the object. If the larger object is picked up or dropped by the player, all of its parts will travel along with it automatically.

One of the advantages of using parts is that in Inform, any single object can be either a container or a supporter, but not both. If our model world includes an object like a chest of drawers, we need to make the chest itself a supporter (because the player may want to put things on top of it), and make its drawers openable containers. Making the drawers parts of the chest is a wise precaution: If you should later change the design of the game to allow the chest of drawers to be moved from place to place, the drawers will come along with it automatically.

Page 8.4 of the _Recipe Book_ has some examples showing how to make furniture. Example 83, “Yolk of Gold,” has a complete implementation of a three-drawer dresser, with the added feature that the player will always find what he’s looking for in the last drawer he opens, no matter which drawer it is.

There are two ways to make something part of something else. We can say:

```inform7
The blade is part of the knife.
```

...or we can say:

```inform7
The knife incorporates the blade.
```

Parts are detachable and attachable objects. This fact can be extremely handy. Let’s suppose, for instance, that in your game you want the player to be able to put a stamp on a postcard:

```inform7
The player carries a postcard and a stamp. Understand "card" and "post card" as the postcard. Understand "postage" as the stamp. The description of the postcard is "A plain white postcard[if the stamp is part of the postcard] with a stamp on it[end if]."

Instead of tying the stamp to the postcard:
        if the stamp is part of the postcard:
                say "You already did that.";
        otherwise:
                now the stamp is part of the postcard;
                say "You lick the stamp and affix it to the postcard."

Test me with "x card / fasten stamp to card / x card / take stamp".
```

You may notice that the action provided by Inform is called tying it to. The player is unlikely to try TIE STAMP TO POSTCARD, but the command would work. The words ATTACH and FASTEN are used by Inform’s parser as synonyms for TIE. If we want the player to be able to use the command PUT STAMP ON CARD, however, we’ll have to do just a little more work:

```inform7
Instead of putting the stamp on the postcard:
        try tying the stamp to the postcard.
```

The main point of the code above is that after the stamp has been attached to the postcard, the player will get this output:

```
>take stamp
That seems to be a part of the postcard.
```

In addition, when the player picks up the postcard and carries it around, the stamp will now be brought along for the ride. To learn how to detach parts of objects, see “Mr Potato Head” in Appendix C, [here](../appendix_c_short_sample_games/mr_potato_head.md#mr-potato-head).

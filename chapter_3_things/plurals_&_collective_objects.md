## Plurals &amp; Collective Objects {#plurals-collective-objects}

As mentioned earlier (in Chapter 2), some objects need to be plural — for example, the tall old trees standing beside the forest path, or the cows grazing in a nearby field. It’s usually not necessary to make every tree a separate object. Instead, we make a single scenery object, and give it the property plural-named. We can do this ourselves, by writing “The tall old trees are plural-named”, or we can let Inform figure it out, by using the word “some”. Let’s create a plural-named object that isn’t scenery:

```inform7
Some scissors are on the sewing table. The description is "The scissors look quite sharp." Understand "sharp", "blades", and "shears" as the scissors.
```

Because we said “Some scissors”, Inform will make the scissors plural-named. So if it needs to mention the scissors — in an inventory list, for instance — it will say “You are carrying some scissors” rather than “You are carrying a scissors.”

If we need to create a collective object, such as sand or water, we can’t use “some” in this way. Here’s the wrong way to do it:

```inform7
Some brackish water is in the pond. [Error!] The water is fixed in place.
```

If the player tries TAKE WATER, the game will respond, “Those are hardly portable.” Instead, we need to do it like this:

```inform7
The brackish water is in the pond. The indefinite article of the brackish water is "some". The water is fixed in place.
```

When we do it this way, by telling Inform what the indefinite article is, Inform understands that the water is not plural-named, but that it should nevertheless say “some water”, not “a water”.

Quite often, we need to write text that will produce outputs for various objects. In this case, we use “[the noun]” or “[a noun]” and let Inform substitute whatever noun is currently being talked about. (The substitutions “[the second noun]” and “[a second noun]” work the same way.) But when we do this, we have to be careful about how we construct the sentence. This looks correct, but it’s a bug:

```inform7
say "[The noun] is too heavy for you to carry." [Error!]
```

If the noun being referred to at the moment happens to be plural-named, the output will be wrong:

```
>take boulders
The boulders is too heavy for you to carry.
```

The old-school solution is to fix this by hand:

```inform7
say "[The noun] [if the noun is plural-named]are[otherwise]is[end if] too heavy for you to carry."
```

Inserting an if-test within text in this way is sometimes an ideal solution to a tricky problem. But when writing messages that may need to refer to things that are plural-named it’s almost always more convenient do this:

```inform7
say "[The noun] [are] too heavy for you to carry."
```

This type of syntax used to require an extension called Plurality by Emily Short, but it now works fine even without that extension, because the concepts in Plurality have been built into Inform.

Page 4.14 of _Writing with Inform_, “Duplicates,” shows how to create collections of indistinguishable items. This is occasionally useful. For example, you might be implementing an old-fashioned money system in which the player can have a purse containing copper pennies, silver dollars, and gold eagles. The coins within each group are identical, so it really doesn’t matter which object the player picks up when using the command PICK UP PENNY.

But precisely because they’re identical, writing code that will move one of them somewhere is slightly tricky. The way to do this is to refer to “a random” object of that kind, in the location where you’re sure one is to be found. Even if there’s only one object of the kind available, you still have to refer to “a random” object of that kind.

Here’s a simple example:

```inform7
The Poultry Shop is a room.

A coin is a kind of thing. Understand "coin" as a coin.
A copper penny is a kind of coin.
A silver dollar is a kind of coin.
A gold eagle is a kind of coin.

The player carries three copper pennies, five silver dollars, and two gold eagles.

The shopkeeper is a man in the Poultry Shop. The shopkeeper carries a duck.

Instead of buying the duck:
        if the shopkeeper carries the duck:
                let P be a random copper penny carried by the player;
                if P is not nothing:
                        now the shopkeeper carries P;
                        now the player carries the duck;
                        say "You buy the duck from the shopkeeper for a penny.";
                otherwise:
        say "'I'll need a penny for this handsome duck,' the shopkeeper says.";
        otherwise:
        say "You've already bought the duck."
```

One thing that’s worth noting about this code is that you have to refer to objects of a kind using the _entire_ term you used when creating the kind. If you write “let P be a random penny” after creating a kind called “copper penny”, Inform won’t know what you’re talking about.

You may want to spend a moment studying how this Instead rule is written. We can safely assume that the player is in a room where the duck is visible, because if there’s no duck, the parser will never need this Instead rule; it will simply reply, “You can’t see any such thing.” So the first question to be asked is, does the shopkeeper still have the duck? Could be yes, could be no. (We will ignore the possibility that the shopkeeper may have hidden the duck under the counter; we’ll assume that the only way he’s going to give it up is if you buy it.) The second question is, does the player still have a penny to spend? Could be yes, could be no.

Trapping all of the logical possibilities is a big part of IF programming.

To return to the main topic of this section, once you’ve created some indistinguishable objects, you’ll quickly discover that the game’s output looks a bit clumsy:

```
>drop dollars
silver dollar: Dropped.
silver dollar: Dropped.
silver dollar: Dropped.
silver dollar: Dropped.
silver dollar: Dropped.
```

There’s nothing really wrong with this except that it looks like a leftover from the 1980s. It doesn’t read well. The extension Consolidated Multiple Actions by John Clemens addressed this issue for earlier versions of Inform. It was not initially compatible with 6L38, but Emily Short has updated it. Hopefully it will be available on the Public Library by the time you read this. Including this extension in your game has no effect on the internal logic of the game (although it does require that the game be compiled to Glulx, so it can’t be used in .z8 games), but it changes the way the action is reported to the player:

```
>drop dollars
You put down the five silver dollars.
```

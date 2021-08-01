## Things Can Have Properties {#things-can-have-properties}

Often, an object can stay the same from the beginning of the game to the end. If the player finds a rock, for instance, that can be used to hammer a nail, probably not too much will happen to the rock during the course of the game. But it sometimes happens that we want to create an object whose state can change during the course of the game because of the player’s action. To keep track of what state the object is in, we need to give it a _property._ “Property” is simply computer programming jargon for an attribute or characteristic. To put it another way, the properties of an object are variables that are stored within the object — variables that may change depending on what the player does with or to the object.

Properties can be of two types. Some of them are numbers, while others are words or groups of words. They’re similar in some ways, but let’s look at them one at a time.

### Number Properties {#number-properties}

Attaching a named number to an object (making it a property of the object) is very simple. To show how it works, we’ll create a lamp that will run out of fuel after a certain number of turns:

```inform7
The player carries a lamp. The lamp is lit. The lamp has a number called fuel-remaining. The fuel-remaining of the lamp is 50.

Every turn:
        if the fuel-remaining of the lamp is greater than 0:
                decrease the fuel-remaining of the lamp by 1;
                if the fuel-remaining of the lamp is 0:
                        now the lamp is not lit;
                        if the lamp is enclosed by the location:
                                say "The lamp flickers and then goes out."
```

Number properties always have names — in this case, “fuel-remaining.” We can manipulate them however we like. If this is an oil lamp, for instance, the player might be able to refill it from an oil can. Here’s a somewhat oversimplified way to do exactly that:

```inform7
The oil can is here. The oil can can be full or empty. The oil can is full.

Refilling is an action applying to one thing. Understand "fill [something]" and "refill [something]" as refilling.

Check refilling:
        say "[The noun] can't be refilled." instead.

Instead of refilling the lamp:
        if the oil can is enclosed by the location:
                if the oil can is full:
                        now the oil can is empty;
                        increase the fuel-remaining of the lamp by 50;
                        say "You drain the oil can into the lamp[run paragraph on]";
                        if the lamp is not lit:
                                now the lamp is lit;
                                say ", and quite magically the lamp's mantle begins glowing brightly again[run paragraph on]";
                        say ".";
                otherwise:
                        say "The oil can appears to be empty.";
        otherwise:
                say "You have nothing to fill the lamp with."
```

This code is oversimplified in several ways. For one thing, I’ve ignored the fact that the player would need a lighted match in order to re-light an oil lamp after it had burned out. Also, we would expect that the player would have to be holding the oil can in order to refill the lamp. The main thing this example is designed to show is the properties fuel-remaining (of the lamp) and full or empty (of the oil can).

### Word Properties {#word-properties}

The easiest way to add word properties to an object is by simply listing the words. In this case, what we have is an anonymous (nameless) property. For instance:

```inform7
The player carries a potato. The potato can be cold, warm, or hot.
```

Presumably the player will be able to do something during the game that will change the temperature of the potato. It’s good practice always to tell Inform what condition you want the object to be in at the start of the game. This removes any possible ambiguity, and makes your code easier to read:

```inform7
The player carries a potato. The potato can be cold, warm, or hot. The potato is cold.
```

If you don’t tell Inform which of the conditions you want the object to start out in, Inform will make an assumption — but its assumption may not be what you intended. Just to make our lives more interesting, if you give the potato’s anonymous property only two possible values (perhaps cold and hot) and fail to tell Inform what state the potato starts out in, the compiler will put the potato in the _second_ of the two states. But if you give a list of three possible states, Inform will initialize the potato object in the _first_ of the possible states.

The method you use to change the state of an object will, of course, depend on the nature of the object and also on the type of puzzle you’re implementing. Here’s a simple example:

```inform7
The blazing fireplace is an open scenery container in the Library.

After inserting the potato into the blazing fireplace:
        now the potato is hot;
        say "You drop the potato into the blazing fireplace, and in a few moments the potato is glowing cherry red and smoldering cheerfully.";
        rule succeeds.

Instead of taking the potato when the potato is hot:
        say "You'd burn your fingers."
```

But letting the player do something that will make the potato hot is only the first step in implementing the puzzle. If the player should happen to refer to the object as a hot potato, the parser will report, “You can’t see any such thing.” So we need to instruct the parser about the vocabulary. Let’s omit, for now, the option of a warm potato, and create one that can be either cold or hot:

```inform7
The potato can be cold or hot. The potato is cold. Understand "hot" as the potato when the potato is hot. The description of the potato is "It's brown and a bit lumpy[if hot]. It's also glowing with heat[end if]."
```

If there are several things in the game that might end up being too hot to pick up because they’ve been put in the fireplace, we might want to write a more general rule, along these lines:

```inform7
Instead of taking something when the noun is hot:
        say "You'd burn your fingers." [Error!]
```

Unfortunately, this doesn’t work as expected. For some reason, Inform will assume that every object has the second value of the anonymous two-state property. Because we said “The potato can be cold or hot,” the parser will assume that _everything_ is hot. We could get around this by saying, “The potato can be hot or cold,” but here’s a safer way to do it:

```inform7
A thing can be hot or cold. A thing is usually cold.
```

Now all of the objects in your game will be explicitly cold, so the general-purpose Instead rule above will work with the potato, the poker, the gold doubloon, or anything else that you let the player put in the blazing fireplace.

But let’s suppose that you want some things to have a variable temperature, while other things don’t need this property. So you decide to be clever. You create temperature as a kind of value, like this:

```inform7
Temperature is a kind of value. The temperatures are cold, warm, and hot.

The Library is a room. A toad is in the Library. The blazing fireplace is an open scenery container in the Library.

The player carries a potato. The potato has a temperature. Understand "hot" as the potato when the potato is hot. The description of the potato is "It's brown and a bit lumpy[if hot]. It's also glowing with heat[end if]."

After inserting the potato into the blazing fireplace:
        now the potato is hot;
        say "You drop the potato into the blazing fireplace, and in a few moments the potato is glowing cherry red and smoldering cheerfully.";
        rule succeeds.

Instead of taking something when the noun is hot:
        say "You'd burn your fingers." [Error!]
```

If you try this miniature game, it will compile, but when you test it with the command TAKE TOAD, you’ll get a run-time error:

```
>take toad

[** Programming error: tried to read (something) **]
Taken.
```

What has happened, in this case, is that the toad doesn’t have a temperature property, so trying to test whether it’s hot (using the Instead rule) can’t possibly work. You might think to try dodging the problem like this:

```inform7
Instead of taking something:
        if the noun provides the temperature property:
                if the noun is hot:
                        say "You'd burn your fingers.";
                otherwise:
                        continue the action;
        otherwise:
                continue the action.
```

This looks perfectly sensible — but it won’t compile. Why? If you look back at the code given a little earlier, you’ll see that temperature isn’t a property. It’s a kind of value. To you and me, the difference between the two ideas may appear trivial, but Inform is fussy about these sorts of things. Fortunately, there’s a solution, which was suggested by Victor Gijsbers. We need to give the potato’s temperature a distinct name, so that it isn’t an anonymous property. Once the property has a name, we can test whether any object possesses that property. The final version is a bit more wordy, but it works as needed:

```inform7
Temperature is a kind of value. The temperatures are cold, warm, and hot.

The Library is a room. A toad is in the Library. The blazing fireplace is an open scenery container in the Library.

The player carries a potato. The potato has a temperature called the heat. Understand "hot" as the potato when the heat of the potato is hot. The description of the potato is "It's brown and a bit lumpy[if the heat of the potato is hot]. It's also glowing with heat[end if]."

```inform7
Instead of taking something:
        if the noun provides the property heat:
                if the heat of the noun is hot:
                        say "You'd burn your fingers.";
                otherwise:
                        continue the action;
        otherwise:
                continue the action.
```

Because we’ve named the property “heat”, we can test whether any object that the player might refer to during the game possesses the property (called) heat.

Giving properties to objects is an extremely useful way of controlling how the objects will function in a game. Number properties are also useful; for more on this topic, you can consult **page 4.12**, “Values that vary,” in _Writing with Inform_. In this section of the _Handbook_ we’ve concentrated on properties that are lists of adjectives. We’ve seen how to create such a list within a single object, how to apply it to all objects, and how to create it as a separate kind of value that may or may not be applied to any given object. We’ve also looked at how to change the description of an object based on the current value of a property and how to let the parser know that a word can be used to describe the object only when the object’s property has a certain value. Finally, we’ve shown how to give a property a name of its own, so as to be able to test whether the object has that sort of property.

## Relations {#relations}

Relations are explained in **Chapter 13** of _Writing with Inform_. They give Inform some extra power, but seeing how best to use that power may not be easy. Relations can do at least two kinds of things, and probably others — I haven’t used them much, so I’m not sure.

First, relations can allow us to write about what’s going on in the model world in ways that are shorter and easier to understand when reading the code. Second, relations can be used to manage how bunches of objects … well, how they relate to one another.

For a couple of examples of the first usage, see **p. 13.9** of _Writing with Inform_, “Defining new assertion verbs.” There, some new verbs are defined, which can then be used in code. Here’s another example, this one my own:

```inform7
Proximity relates a thing (called X) to a thing (called Y) when the holder of X is the holder of Y. The verb to jostle (he jostles, he jostled, it is jostled, he is jostling) implies the proximity relation.
```

If you need to make a decision in the game based on whether two objects are in the same container, or on the same supporter, or in the same room (directly in the room — on the floor), or carried by the same person, you would normally write something like this:

```inform7
if the holder of the apple is the holder of the orange:
```

But after creating a proximity relation as shown above, you can simplify this test a bit by writing:

```inform7
if the apple jostles the orange:
```

I’ve defined the word “jostles” using a relation. Any unused word would serve — “snuggles” or “elbows”, for instance (but probably not “is able to touch”, since Inform already knows how to test whether a character “can touch” an object).

Various Examples in Chapter 13 of _Writing with Inform_ show how the interactions among groups of people can be managed using relations. These examples are worth studying in detail. If you’re wondering whether it would be worth your while to spend the time on it, here’s an imaginary example that may make the use of relations slightly easier to understand.

Imagine a game in which the player plays the part of Cupid, complete with bow and arrow. To win the game, you need to shoot Jason with an arrow, shoot Jennifer with an arrow, and then get Jason and Jennifer into the same room so that they fall in love.

If they wander into the same room, the software will need to be able to figure out whether each of them has been shot with an arrow and is ready for love. That’s the easy part. All we need to do is write a few assertions along the lines of “A person can be ready-for-love.” If Jason has been shot and is ready-for-love, he’ll fall in love with Jennifer when he sees her (assuming we write code that will make him do so). But Jennifer might not have been shot yet, so she might not fall in love with Jason when she sees him.

There’s no real need to use relations to manage this game. You can do something simple, with properties, like this:

```inform7
Jason can be ready-for-love or not ready-for-love. Jason can be loving-Jennifer or not loving-Jennifer.
```

...and similar properties for Jennifer. When Jason is loving-Jennifer and Jennifer is loving-Jason, the player has won the game. We don’t need relations here, because these two properties will do the job nicely.

But now imagine that the game includes Steve, Bill, Ted, Ralph, and Jason; and also Jennifer, Susan, Beth, Amy, and Helen. Any of the men can fall in love with any of the women, and vice-versa! (In the interest of not offending our more traditionally minded readers, we’ll ignore the other possibilities.) If we try to use properties, the list of properties each character will need is going to be rather long, and managing these properties in such a way as to avoid bugs will be quite tricky. To manage the potential romantic tangles that can arise during the game in a more reliable way, a better approach will be to use relations.

The code for this game would almost certainly include the example sentence on **p. 13.5**, “Loving relates various people to one person.” We would have to write more code in order to cause characters who have been shot with one of Cupid’s arrows to fall in love with the next suitable person they see. I’m not going to do that here, but it’s not actually a bad idea for a game. I hope someone will try it. Once a character is ready-for-love and sees an appropriate romantic object, all we need to write is:

```inform7
now Steve loves Susan;
```

If Steve has previously been in love with Amy, that one line of code will automatically make him fall out of love with Amy, because the statement “Loving relates various people to one person” allows a person to love only one other person at a time. That’s the power of relations: Relations can manage the various combinations a lot more easily.

If you’re using relations in your game, you can take advantage of the debugging command RELATIONS, which prints out a list of all the relations that are currently active among the objects in your game.

Here’s a more complete (and more practical) example of how to use relations. In this short game, we want the player to have to stand on a chair in order to touch the chandelier. But it’s not enough to stand on the chair: The chair has to be positioned correctly beneath the chandelier. In addition to a new action (putting it beneath), we need to define a relation that will keep track of whether something is beneath something else. Whenever the player picks up an object, we need to get rid of the relation. And just to keep things tidy, we’ll also create a new property, high or low. The player will only be able to put things beneath things that are high. In a game where the player is allowed to put a coaster underneath a glass, or a silver dollar underneath a sofa cushion, the high/low property might get in the way, and the rules for the putting it beneath action would naturally be more complicated. But this example could easily be adapted so as to force the player to put a chair beneath a high shelf in order to get something off of the shelf, for example.

```inform7
A thing can be high or low. A thing is usually low.

The Living Room is a room. "A large, old-fashioned room lit by a crystal chandelier."

The crystal chandelier is scenery in the Living Room. The description is "It shimmers with light." The chandelier is high.

The chair is an enterable supporter in the Living Room. It is not fixed in place. The description is "A sturdy chair[if the chair is near the chandelier]. It's positioned directly beneath the chandelier[end if]."

Proximity relates things to each other. The verb to be near implies the proximity relation.

Putting it beneath is an action applying to two things and requiring light.

Understand "put [something] underneath/beneath/under [something]", "push [something] underneath/beneath/under [something]", "place [something] underneath/beneath/under [something]", "set [something] underneath/beneath/under [something]", and "position [something] underneath/beneath/under [something]" as putting it beneath.

Check putting it beneath:
        if the second noun is not high:
                say "[The second noun] lack[if the second noun is not plural-named]s[end if] the requisite elevation." instead.

Carry out putting it beneath:
        now the noun is in the location;
        now the noun is near the second noun.

Report putting it beneath:
        say "You place [the noun] on the floor directly beneath [the second noun]."

Instead of putting the chair beneath the chandelier:
        if the chair is near the chandelier:
                say "The chair is already beneath the chandelier.";
        otherwise if the player is on the chair:
                say "You'll have to get off of the chair if you want to do that.";
        otherwise:
                if the player carries the chair:
                        move the chair to the location;
                now the chair is near the chandelier;
                say "You place the chair beneath the chandelier."

After taking something:
        if the noun is near a thing:
                now the noun is near nothing;
        continue the action.

Check touching the chandelier:
        if the player is not on the chair:
                say "You can't reach it." instead;
        otherwise if the chair is not near the chandelier:
                say "It's out of reach. Maybe if you put the chair underneath the chandelier first, you could reach the chandelier." instead.

Report touching the chandelier:
        say "The crystal is cool to the touch, and a little dusty. The entire chandelier sways gently as your fingers brush it, and makes a soft, musical tinkling sound.";
        rule succeeds.

The player carries a bowling ball. [For testing purposes.]

Test me with "touch chandelier / stand on chair / touch chandelier / get off / put chair under chandelier / stand on chair / touch chandelier / put ball under chandelier / relations".
```

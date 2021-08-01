## Transforming One Thing into Another {#transforming-one-thing-into-another}

In a game that includes magic, you might want to turn an object into another object. (Maybe this would happen when you cast a spell on the object using my Spellcasting extension.) The easy way to do this in Inform is to create both objects but leave one of them offstage at the beginning of the game. When it’s time to transform the object, simply whisk it offstage and replace it with the other object. Here’s the classic story situation, more or less:

```inform7
The Creekside is a room. "A burbling creek runs through the forest here."

The toad is an animal in the Creekside. "An ugly, warty toad squats on a rock near the creek." The description is "He's ugly and green." Understand "ugly" and "green" as the toad.

The princess is a woman. "A beautiful princess stands before you!" The description is "She's the most beautiful woman you've ever seen." Understand "beautiful" and "woman" as the princess.

Instead of kissing the toad:
        now the princess is in the location of the toad;
        now the toad is nowhere;
        say "As your lips touch the ugly toad, it shimmers and sparkles and turns into a beautiful princess. 'My goodness,' the princess declares. 'Thank you!'"

Instead of kissing the princess:
        say "The princess smiles modestly and pushes you away. 'Maybe later,' she suggests. 'After we get to know one another better.'"
```

Initially the princess is nowhere. The Instead rule does three things. First, it makes a note about where the toad is. This is a good idea, because in a real game the toad might be moving around, and it would be a bug if you kiss the toad in the throne room and have the princess pop up back at the creekside. Then the rule gets rid of the toad and moves the princess to the room where the toad was.

If we’re transforming one inanimate object into another, we’ll want to do it just a bit differently, because an inanimate object might be on a supporter or in a container. If you’re transforming a gold crown into an old shoe, for instance, and if the crown is on a table, you don’t want the shoe to appear on the floor of the room — you want it to show up on the table. To take care of this, we need to refer to “the holder” of the crown. The holder will always be the crown’s immediate location:

```inform7
Instead of casting shazam at the crown:
        now the old shoe is in the holder of the crown;
        remove the crown from play;
        say "The crown emits an unhappy crinkling, shriveling sort of noise, and turns into an old shoe."
```

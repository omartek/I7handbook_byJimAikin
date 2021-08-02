## Deceptive Appearances & Unusual Usages {#deceptive-appearances-unusual-usages}

An object with a deceptive appearance is different from an object whose description is poorly written (see “Inadequate Implementation,” below). The initial description of an object might be vague because the PC has never seen anything like it and doesn’t know what it is, or because only part of it is present, thus giving it an enigmatic shape, or because it is in an odd condition.

As a simple example, consider an object called “a wadded-up piece of paper”. This is quite likely a deceptive appearance. If you try READ PAPER, you’ll probably be told, “You can’t read a wadded-up piece of paper!” However, commands like SMOOTH PAPER and UNFOLD PAPER will probably change the name of the item to “a slightly wrinkled note”, after which READ PAPER or READ NOTE will reveal what’s written on it.

A variant of the unusual usage puzzle is what we might call the unexpected action puzzle. This isn’t quite the same as a guess-the-verb puzzle, because the author has done it on purpose. Suppose, for instance, that you’ve got a little glass bottle with some tablets in it. The top of the bottle is stuck tight, so OPEN BOTTLE simply doesn’t work. However, BREAK BOTTLE might be the intended solution of the puzzle. This particular example also fits in the locked container category. A better example might be an object described as “a small tarnished piece of metal.” The command POLISH METAL might turn this object into a mirror which which you could direct a beam of light. To implement this, you’d also want to change the object’s printed name property. A better solution, especially if the mirror is going to be useful as a solution to a later puzzle, is to whisk the tarnished piece of metal off-stage and replace it with a new object that has been waiting in the wings. The rubbing action already has “polish” as a synonym, so we can write this:

```inform7
The player carries a small tarnished piece of metal. The description is "It's rather corroded."

The polished hand mirror is a thing. The description is "A gleaming smooth mirror, small enough to fit in the palm of your hand."

Instead of rubbing the piece of metal:
        now the piece of metal is nowhere;
        now the player carries the polished hand mirror;
        say "As you rub the corrosion from the piece of metal, its true identity is revealed: It's a hand mirror!"
```

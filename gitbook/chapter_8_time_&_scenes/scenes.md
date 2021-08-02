## Scenes

One of the more powerful features of Inform is its ability to organize the story into scenes. An entire chapter of _Writing with Inform_ (Chapter 10, “Scenes”) is devoted to scenes. If you haven’t read this chapter yet, give it a look. Some games won’t need scenes at all, but scenes can be very handy for giving your story some structure. Almost any time you need to create a complex, well-coordinated set of changes in the model world, defining a scene is a good tool for the job.

To create a scene, you simply give it a name, and then tell Inform when it starts — that is, what set of events or circumstances triggers it. You can also, optionally, tell Inform when the scene ends. By default, a scene will happen only once. If you want it to be able to happen over and over, you need to create it as a _recurring_ scene.

Why might you want to use a scene? Here are some random ideas:

```inform7
Saucer-menace is a scene. Saucer-menace begins when the flying saucer is in the Meadow. Saucer-menace ends when the bug-eyed monster is dead.

Guard-evasion is a scene. Guard-evasion begins when the security guard is suspicious. Guard-evasion ends when the player is in the Bank Vault for the first time.

Dance mania is a scene. Dance mania begins when the player is in the Abandoned Warehouse for the first time. Dance mania ends when the police sergeant is in the Abandoned Warehouse.
```

When a certain scene starts, you might want to rearrange the objects in the model world, shuffling some items offstage and others onstage. While the scene is happening, you might want to restrict the player’s travel, or print out certain atmospheric messages (as shown on **p. 10.4** of _Writing with Inform_, “During scenes”). While a scene is happening, the magical weapons the player is carrying might have different effects than at other times. The possibilities are unlimited.

You can’t start a scene simply by saying that it starts:

```inform7
now guard-evasion is happening; [Error!]
```

Nor can you end a scene by saying that it ends. The way to start or end a scene is to tie it to a condition, as shown above:

```inform7
Guard-evasion begins when the security guard is suspicious.
```

The condition can be as simple as whether a truth state that varies (a true-or-false variable) is true or false. You could do it this way:

```inform7
Guard-evasion-flag is a truth state that varies. Guard-evasion-flag is false.
Guard-evasion is a scene. Guard-evasion begins when guard-evasion-flag is true.
```

Having set it up this way, you can start the scene whenever or wherever you like by writing:

```inform7
now guard-evasion-flag is true;
```

### Chaining Scenes

**Page 10.5** of _Writing with Inform_, “Linking scenes together,” gives this simple example of how to chain two scenes:

```inform7
Train Stop is a scene. Brief Encounter is a scene. Brief Encounter begins when Train Stop ends.
```

From this code, we can’t tell what events will cause Train Stop to begin or end, but we can see that Brief Encounter will begin immediately when Train Stop ends.

Setting up a new scene so that it starts a certain number of turns after a previous scene ends is a little trickier. First, we need to create a truth state. Second, we need to write a simple function that will switch the truth state to true. Third, we need to tell Inform to run the function at some time in the future. Here’s an example that shows how to do it:

```inform7
The Sidewalk Cafe is a room.
The Wine Shop is north of the Sidewalk Cafe.

Lunch-ready is a truth state that varies. Lunch-ready is false.

Breakfast is a scene. Breakfast begins when play begins. Breakfast ends when the player is in the Wine Shop for the first time.

When Breakfast ends: The gong sounds in three turns from now.

At the time when the gong sounds:
        now lunch-ready is true.

Lunch is a scene. Lunch begins when lunch-ready is true. When Lunch begins, say "Luncheon is served."

Test me with "scenes / n / z / z / z".
```

The phrase “The gong sounds” is entirely artificial. You could use anything here; there isn’t any gong in the game. It’s just a way of lining up an event to occur in the future. When the player enters the Wine Shop, it causes the Breakfast scene to end. Three turns later, the Lunch scene begins.

We could just as easily skip the truth state and the delayed sounding of the gong like this:

```inform7
Lunch begins when the player has been in the Wine Shop for three turns.
```

But if we do it that way, the player will have to remain in the Wine Shop for three turns in a row. If the player leaves the Wine Shop too soon, the Lunch scene won’t begin.

### Using Scenes to Control Action

Here’s a rather convoluted but interesting example of how useful scenes can be. At the beginning of this little game, the player carries the crown jewels. If the player goes into the boudoir, where the princess is waiting, the princess won’t let the player leave until the jewels have been handed over. This situation is similar to the example on p. 195, in which Wyatt Earp demands that the player hand over his six-gun, but we’ll set it up using a different kind of code.

```inform7
The Antechamber is a room. "The princess's boudoir lies to the south."

The Princess's Boudoir is south of the Antechamber. "This luxuriously appointed chamber is fit for a princess."

The princess is a woman in the Boudoir. "...and as it happens, a princess is sitting here right now!"

The player carries some crown jewels. The indefinite article of the crown jewels is "the".

Princess Demanding is a recurring scene. Princess Demanding begins when the player is in the Boudoir and the player carries the crown jewels.

Princess Demanding ends when the player does not carry the crown jewels.

Instead of going during Princess Demanding:
        say "'You're not going anywhere until you surrender the jewels!' the princess insists."

When Princess Demanding begins:
        say "'I notice you're carrying the crown jewels,' the princess says. 'Give them to me at once!'"

Instead of giving the jewels to the princess:
        now the princess carries the jewels;
        say "You surrender the jewels. The princess smiles sweetly. 'Thank you,' she says. 'You may go.'"
```

Here we’ve created a scene called Princess Demanding. The point of this scene is the “Instead of going” rule. This rule gets in the way if the player tries to leave the boudoir with the jewels. Other than this, the scene is transparent — that is, it has no effect on game-play. The player can drop the jewels or give them to the princess. At that point, the scene ends (because we’ve written a rule that defines this as ending the scene).

The keyword “during” in this Instead rule lets us write code that will make sweeping changes in many aspects of the game depending on whether a certain scene is happening.

We’ve made Princess Demanding a recurring scene. This is necessary. If you leave out the word “recurring,” the player can get away with the jewels by dropping them in the boudoir and then picking them up again. When they’re dropped, the scene ends — and if it’s not a recurring scene, it will never start again.

Let’s look at this scene more closely. It looks sensible on the surface, but in fact there are some problems. By analyzing the problems, you can start to get a better picture of how to write trouble-free code.

In a real game the player would quite likely be able to figure out a way to abscond with the jewels, even after the princess has noticed them. Can you spot the problem? If you’ve read the section in Chapter 3 on “Testing Where a Thing Is,” you may recall that the condition “if the player carries the crown” is only true if the crown is in the PC’s hands — that is, if it’s directly carried. The bug will show up if we give the player a container for carrying things:

```inform7
The sack is a container. The player carries the sack.
```

Now the player can walk into the boudoir, which will cause the princess to notice the jewels, and then put the jewels in the sack and walk straight out again. Oops! The fix for this bug is simple. We change “carries” in the end-of-scene statement to “encloses”:

```inform7
Princess Demanding ends when the player does not enclose the crown jewels.
```

If you make these changes, the player will be able to put the jewels in the sack and then enter the boudoir, and the princess will let him leave again. Presumably, she hasn’t noticed the jewels because they’re in the sack. But once the jewels are not in the sack but in the PC’s hands, she’ll see them. At that point, putting them back in the sack won’t help. The princess will still demand that they be turned over.

But there’s still a problem. Try this series of commands:

```inform7
Test me with "s / put jewels in sack / drop sack / take sack / n".
```

The princess will notice the jewels ... but you can still get away with them by putting them in the sack, dropping the sack, and picking it up again, because the Princess Demanding scene won’t start again as long as the jewels are in the sack. Ah, but we don’t want to change the definition of the start of the scene so that it uses “encloses” rather than “carries,” because that would cause the princess to notice the jewels for the first time even if they’re in the sack. What a tangle!

The solution is in two parts. First, we need to keep track of what the princess knows. In addition, we’ll create a second scene, Princess Still Demanding. This scene will do the work of stopping the player from leaving — and it will have a more complicated beginning. Here’s the revised part of the code:

```inform7
The princess is a woman in the Boudoir. "...and as it happens, a princess is sitting here right now!" The princess can be jewel-knowing or jewel-ignorant. The princess is jewel-ignorant.

When Princess Demanding begins:
        now the princess is jewel-knowing.

The player carries some crown jewels. The indefinite article of the crown jewels is "the".

The sack is a container. The player carries the sack.

Princess Demanding is a scene. Princess Demanding begins when the player is in the Boudoir and the player carries the crown jewels.

Princess Still Demanding is a recurring scene. Princess Still Demanding begins when the player is in the boudoir and the player encloses the crown jewels and the princess is jewel-knowing.

Princess Demanding ends when Princess Still Demanding begins.

Princess Still Demanding ends when the player does not enclose the crown jewels.

Instead of going during Princess Still Demanding:
        say "'You're not going anywhere until you surrender the jewels!' the princess insists."
```

The first thing we’ve done here is give the princess a new either-or property. She can be jewel-knowing or jewel-ignorant. At the beginning of the game she’s jewel-ignorant. But when Princess Demanding begins, she becomes jewel-knowing. The moment she becomes jewel-knowing, the game switches to a different scene, Princess Still Demanding.

If you add this code to the original version of the example, the player will be able to go in and out of the boudoir freely carrying the jewels in the sack. But once the princess spies the jewels, the player will be prevented from leaving whether the jewels are directly carried or are being carried in a container.

There’s still at least one more problem with this example game, which illustrates just how tricky writing IF can be. If the player drops the jewels on the floor, the princess will just leave them lying there. She’ll let you leave, but if you leave the boudoir and come back, you’ll find that the jewels are still lying on the floor in plain sight. A writer of conventional fiction might describe this by saying that the princess’s motivation (her reasons for her actions) is not consistent. We can fix this with an Every Turn rule:

```inform7
Every turn:
        if the holder of the crown jewels is the Boudoir:
                now the princess carries the crown jewels;
                say "The princess scoops up the jewels. 'These belong to my family,' she says, adding haughtily, 'you may go.'"
```

As an exercise, I’ll leave you the chore of setting it up so that if the princess is jewel-knowing, the jewels are in the sack, and the sack is on the floor of the boudoir, the princess will take the jewels from the sack. The moral of the story is this: When planning an action, think about _all_ of the actions a player might take. Think about all of the configurations the various objects might get into. Also, think about how any other characters in the room would naturally react when the PC does something or other.

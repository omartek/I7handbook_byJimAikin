## Inventory {#inventory}

When the player types INVENTORY, INV, or simply I, Inform will print out a list of what the player is carrying or wearing. This list can be formatted in various ways — as a column, as a sentence, and so on. For details on how to do this, see **p.** 6.7 of the _Recipe Book,_ especially Example 177, “Equipment List.”

If you’re writing a game that tries to be realistic, allowing the player to carry 20 or 30 things at once is a bit silly (unless the player character is an alien with 20 or 30 hands). Some game authors prefer to limit the number of items the player can carry at once. As explained on **p. 3.19** of _Writing with Inform_ (“Carrying capacity”), we can easily set this up by saying:

```inform7
The carrying capacity of the player is 5.
```

Players don’t like having a limited carrying capacity, because it’s a huge hassle to have the game keep telling them, “You’re carrying too many things already” when they try to pick up something new. The solution is to put a **holdall** container somewhere in the game — preferably in a place where the player will find it early in the game. The holdall could be a shopping bag, a backpack, a burlap sack, or whatever fits with your story. Creating a holdall is easy:

```inform7
The backpack is an open container in the Barn. The backpack is a player’s holdall.
```

When this container is added, here’s what happens as the player tries to load down with more objects than the carrying capacity. In this example, the carrying capacity of the player is 5. The player is already holding the backpack and the flaming torch.

```
You can see a banana, a peach, a kumquat, a pear, an apple, an orange and a bowling ball here.

>take all
banana: Taken.
peach: Taken.
kumquat: Taken.
pear: (putting the banana into the backpack to make room)
Taken.
apple: (putting the peach into the backpack to make room)
Taken.
orange: (putting the kumquat into the backpack to make room)
Taken.
bowling ball: (putting the pear into the backpack to make room)
Taken.

>i
You are carrying:
a bowling ball
an orange
an apple
a flaming torch (providing light)
a backpack (open)
  a pear
  a kumquat
  a peach
  a banana
```

If the player is carrying the holdall, when the player tries to pick up too many things at once, Inform will shuffle the excess items into the holdall automatically, like this:

Considerate Holdall by Jon Ingold is an extension that improves on Inform’s basic concept of a holdall. At present (February 2015) it’s not compatible with 6L38, but editing it turns out to be not a huge problem. (See Appendix B.) One useful thing that this extension adds is the idea that the author can insist that certain things ought not to be shuffled into the holdall at any time. If the player is carrying, say, a small rodent or a plate of cookies, stashing them in the holdall would probably be a bad idea. Even without this extension, Inform will understand that something providing light (such as a flaming torch) shouldn’t be deposited in the holdall — but it will have no hesitation about tossing the rodent in with the plate of cookies.

If you want to make your game more realistic, you may want to think not just about the sheer number of items the player may want to pick up, but about their bulk. The extension called Bulk Limiter by Eric Eve allows you to assign a bulk to any object and a bulk capacity to any container. This extension is handy for a couple of reasons. With a little care, you can prevent silly things like having the player put a chair in his pocket. And if there are numerous bulky objects around (say, a chair, a string bass, and a shipping trunk), you can easily set the game up so that the player will only be able to carry one of them at a time. Your code might look something like this:

```inform7
The bulk capacity of the player is 65.
The bulk of the chair is 45.
The bulk of the string bass is 50.
The bulk of the shipping trunk is 40.
```

Bulk Limiter is not a perfect solution to all problems of this sort. It doesn’t give us any tools with which to handle long, thin objects that might not fit into a container. Also, if the player is prevented from picking up something bulky while carrying several things that are small, Bulk Limiter will just refuse the action; it won’t shuffle the small things into a holdall automatically.

>Things to Think About
>
>In the simplest interactive fiction games, every portable thing in the game is useful for solving one puzzle. After the player has figured out that he can use the bent hairpin to unlock the jewel box, he can safely discard the hairpin, because it won’t be needed again. Your game will be more interesting for players if you add variety to this scheme.
>
>- Two or three of the things you create might have multiple uses.
>
>- Two or three of your puzzles might have two solutions using different things.
>
>- One or two objects might be _red herrings._ They might not be good for anything at all.
>
>- One object or obstacle that appears to be a puzzle might also be a red herring. It have no solution at all.

## Broken Eggs

This next example was originally written by Jason Travis and posted in the newsgroup, in response to a question from Rob Cowell about how to break a box full of eggs when the box was dropped. I’ve expanded the example quite a bit. It shows how to handle a collection of indistinguishable objects (the eggs) when any individual egg can be either broken or unbroken.

First, we’ll set up the game and let Inform know that an egg is a kind of thing. We’ll add some code that will allow eggs to be broken or unbroken. Note the use of a couple of “before printing” rules to let the player know what sort of egg is being mentioned. This is a handy alternative to changing the printed name of an egg object when the egg itself is in the process of getting broken.

```inform7
"Humpty Dumpty Doesn't Live Here" by Jason Travis &amp; Jim Aikin

The story headline is "A heart-rending tale of clumsiness and its irreversble consequences,"

The Kitchen is a room. "A well-appointed kitchen with all sorts of things you really don't need to interact with."

An egg is a kind of thing. An egg can be unbroken or broken. An egg is usually unbroken. The description is "[if unbroken]Ovoid and whitish.[otherwise]Yolk and other stuff grotesquely splashed in an interesting pattern among various sharp bits of shell."

Understand the unbroken property as describing an egg.

Understand "sharp", "bits", "shell", "yellow", and "yolk" as broken. Understand "whole", "white", "whitish", "ovoid", and "fresh" as unbroken.

Before printing the name of a broken egg, say "broken ".

Before printing the plural name of a broken egg, say "broken ".
```

We don’t want the player carrying around broken eggs, so we’ll get rid of them if the player tries to take them. This next bit of code illustrates the use of the word “called” to create a reference (BE) that we can use while writing the Instead rule. In this case, we could just as easily skip the “called” reference and say “remove the noun from play”, but “called” is a handy bit of syntax to know, so we’ll use it here.

```inform7
Instead of taking a broken egg (called BE):
        say "You spend a good deal of time cleaning it up, throwing the gooey debris into the trash.";
        remove BE from play.
```

Next, we need a box with some eggs in it. Note the use of the text substitution “[box-contents]”. This lets us write a whole To say rule that will mention the eggs in the box if there are any. By default, Inform doesn’t list the contents of an open container when the container is examined. But since broken eggs are highly noticeable, we’ll tack a list of things in the eggbox onto the description. The carry out rule for examining the eggbox causes Inform not to print out an extra line repeating the contents of the box. This is not strictly necessary; we could let Inform do this for us. But it would make the list of contents into a separate paragraph. The code below tucks the list of contents neatly into the end of the main paragraph.

```inform7
The eggbox is a closed openable container in Kitchen. The description is "It is made of recycled paper, and is decorated with a garish cartoon showing a line of happy chickens with their wings wrapped across one another's shoulders as they dance the can-can[box-contents]." The eggbox contains six eggs. Understand "box", "recycled", "paper", "happy", "chickens", and "carton" as the eggbox.

Carry out examining the eggbox:
        say "[description of the eggbox][line break]";
        rule succeeds.

To say box-contents:
        if the eggbox is closed:
                do nothing;
        otherwise if the number of things in the eggbox is 0:
                do nothing;
        otherwise:
                say ". In the box you can see [a list of things in the eggbox]".

```

Now it’s time to break some eggs. The first part is easy. If the player uses the command DROP EGG, something bad will happen. We’ll break the egg in an After rule because we want to make sure the dropping action has been successfully carried out. If we used an Instead rule, we’d have to move the broken egg to the floor of the room manually, because the Instead rule would bypass Inform’s normal handling of the DROP action. We’d also have to make sure the player was actually carrying the egg, for the same reason. With an After rule, our code can be simpler and less error-prone.

The consequences of dropping the eggbox are more complicated. We’re going to assume that if the eggbox is closed, the eggs in it won’t break when the box is dropped. (Kids — don’t try this at home!) If the box is open, the eggs in it will break. But what if the box contains both some broken eggs and some unbroken ones? That could happen, for instance, if the player uses the commands OPEN BOX, TAKE EGG, DROP BOX, PUT EGG IN BOX, TAKE BOX. At this point the box would contain (probably) some broken eggs and an unbroken one.

```inform7
After dropping an egg (called E):
      	now E is broken;
      	say "The egg tumbles to the floor in slow motion, breaking apart spectacularly. Somewhere in the distance you hear the forlorn cluck-cluck-cluck of a mother hen."

After dropping the eggbox:
      	if the eggbox is closed:
            		if the eggbox does not contain an egg:
                  			say "The empty box skitters across the floor.";
            		otherwise if the eggbox contains a broken egg:
                  			say "The eggbox makes a sort of squishy, sloshing sound as it hits the floor.";
            		otherwise:
                  			say "You hear [the number of eggs in the eggbox in words] egg[s] jouncing around safely in the carton.";  
      	otherwise:
            		if the eggbox does not contain an egg:
                  			say "The empty box thunks hollowly on the floor.";
            		otherwise if the eggbox contains an unbroken egg:
                  			say "Whoops! Broken [run paragraph on]";
                  			if the number of unbroken eggs in the eggbox is greater than 1:
                        				say "eggs.";
                  			otherwise:
                        				say "egg.";
                  			now every egg in the eggbox is broken;
            		otherwise:
                  			let N be the number of broken eggs in the eggbox;
                  			say "The broken egg[if N is greater than 1]s slosh[otherwise] sloshes[end if] around viscously in the eggbox as it hits the floor."
```

Studying this After rule may help you see how to structure blocks of code. The outermost if-test is “if the eggbox is closed … otherwise”. Within each of these blocks, we test whether the eggbox does not contain an egg, and deal with that possibility. And so on.

The use of “[run paragraph on]” and “let N be the number...” is also worth a quick look, if you’re not familiar with these tools.

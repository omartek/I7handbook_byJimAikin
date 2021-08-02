## Scenery {#scenery}

Inform allows us to create many kinds of objects. The standard library includes containers, mechanical devices, doors, people, and so on. (See Chapter 4 of the Documentation, “Kinds,” to learn more about kinds.) The word “kind” is a technical term in Inform: It’s used to define new types of objects when the game will include several of them, and we want them to behave in similar ways. For instance, if a puzzle involves spelling words with alphabet blocks, we might do this:

```inform7
An alphabet block is a kind of thing.
```

After writing this, we could write rules that would apply to all alphabet blocks, and Inform would know what we were talking about. A trap that beginning Inform authors sometimes fall into is to use the word “kind” in the casual way that an English speaker would use it. For example:

```inform7
A leopard is a kind of animal.
```

Inform knows what an animal is, so this sentence will compile. But oddly enough, the sentence doesn’t create an object called a leopard. It creates a _kind_ of object, on the assumption that you will later be writing about a small leopard, a large leopard, a spotless leopard, and a leaping leopard (or whatever), and that you plan to write some code that will be used by all of the objects of the leopard kind. If you want to create only one actual leopard, don’t use the word “kind”:

```inform7
A leopard is an animal.
```

The first type of object we’re going to meet in this book is scenery. To make matters a little more confusing, however, the word “scenery” in Inform does not refer to a _kind_ of object at all; it’s a property that can be applied to almost any object. A thing (the basic kind) can be scenery; a container or supporter can be scenery; a door can be scenery; a device can be scenery; and so on. Things, containers, supporters, doors, and devices are all different kinds.

If we don’t say anything more specific when creating scenery, Inform assumes that the object we’re creating is just an ordinary thing, not a device, door, or container. It also assumes that scenery is fixed in place: that it’s not something the player can pick up and carry around.

When your game is constructing a room description to print out, it will mention any ordinary objects that are lying around in the room, but it won’t mention scenery objects (unless the object is a supporter that has something else sitting on it; see [here](../chapter_3_things/containers_&_supporters.md#containers-supporters) for more on supporters). Inform assumes that you mentioned the scenery objects in your own room description when you wrote it, so be sure to do so.

We can add scenery to our forest path like this:

```inform7
The Forest Path is a room. “Tall old trees surround you.”

The tall old trees are scenery in the Forest Path. The description is “Ancient oaks stretch out their heavy branches overhead, blocking the sun.”
```

Now the player who types X TREES will be able to read a description that adds detail to the scene. Notice that here I’ve started the sentence by saying:

```inform7
The description is [… and so on …]
```

The phrase “The description is” is optional with scenery and rooms, but it’s _required_ with objects that can be picked up and moved around (as described in Chapter 3). If you don’t use “The description is” with scenery, you should be sure to always put the description in the very next sentence after you’ve created the scenery object. The code below works exactly like what was shown above — but only with scenery, not with ordinary things.

```inform7
The tall old trees are scenery in the Forest Path. “Ancient oaks stretch out their heavy branches overhead, blocking the sun.”
```

### The Names of Things {#the-names-of-things}

If you try out this code, you’ll soon discover two problems. First, you can X TREES, X TALL TREES, or X OLD TREES, because the scenery object was created with the name “tall old trees,” but you can’t X OAKS or X ANCIENT OAKS. The parser will reply, “You can’t see any such thing,” which is fairly silly. It happens — and this is important — because Inform never looks inside of double-quoted text to see what words you used there. Second, if you should try something like TAKE TREES, the parser will complain, “That’s hardly portable.” The word “trees” is plural, so the correct output would be “Those are hardly portable.” But the parser doesn’t know that the trees object is plural. We have to help it out a little.

To solve the first problem, we’ll add an Understand rule to the trees. You’ll soon find that most of the objects you create in your games will need Understand rules of this type. Their main purpose is to add vocabulary — extra words that the player can use to refer to the objects. (The concept of rules is vital to Inform. You’ll write many rules in your own code, and you’ll see them used throughout this _Handbook_. For more details, consult Chapter 19 of _Writing with Inform._)

To solve the second problem, we need to make sure the parser understands that the tall old trees object is **plural-named**. There are two ways to do this. We can do it explicitly, by adding the sentence, “The tall old trees are plural-named” to our source. Or we can do it implicitly, by changing the sentence where we create the trees so that it refers to “Some tall old trees”. The second method is easier. Inform knows that when things are created using the word “some”, they’re plural-named. When we put it all together, the trees will look like this in our source code:

```inform7
Some tall old trees are scenery in the Forest Path. “Ancient oaks stretch out their heavy branches overhead, blocking the sun.” Understand “ancient”, “oaks”, “heavy”, “branches”, “branch”, and “tree” as the tall old trees.
```

Notice that when we add vocabulary words to the trees object, we have to put the commas that separate items in the list of words _outside_ the quotation marks.

This usage of “some” to create a plural-named object is convenient, but there’s a potential problem to be aware of. In English, some nouns are “collective.” Examples would include things like sand and water. If we write “Some sand is scenery in the Beach,” Inform will be confused into thinking the sand is plural-named. If it needs to construct a sentence that includes the sand object, it will say “The sand are....” To avoid this, we need to create the sand using “the”, not “some” — and then we need to tell Inform to refer to the sand as “some sand” when it needs to construct a sentence, not as “a sand”. Here’s how to do it:

```inform7
The sand is scenery in the Beach. The indefinite article of the sand is "some".
```

The term “indefinite article” refers, in English, to the words “a” and “an”. See **p. 3.18** of _Writing with Inform_, “Articles and proper names,” for more on this technique.

Once we’ve created the tall old trees as a scenery object, we can refer to the object in our source code either as “tall old trees” or just as “trees”. The compiler will understand either form. However, You may want to get in the habit of always using the full names of objects when writing your game. If you use the short forms of names, Inform will usually understand what you meant, but it’s possible to end up with code that includes hard-to-find bugs.

The reason is this: You may have several objects in your game whose name ends with the noun “trees” — the tall old trees in the forest, the pear trees in the orchard, and the shoe trees in the closet. If you just say “trees” in your source code, the compiler will try to figure out which object you meant, and it will usually get it right. But once in a while it will get confused. The result could be disastrous: The player might try to pick up the shoe trees and end up carrying around the whole forest or the orchard by mistake.

For the same reason, it’s a good idea to get in the habit of naming every object with at least one adjective in addition to the noun. Odd things can happen if you have one object called the beach ball and another object that’s simply called the ball.

In case you’re wondering — no, it’s not possible to refer to the tall old trees in your own source code as “the ancient oaks”. Words in Understand rules are strictly for the player’s convenience, not for the author’s use.

At the beginning of the game, players don’t know what’s important. So they’ll try out anything they can think of. With the tall old trees, we can expect the player to try CLIMB TREES (or more likely, CLIMB TREE, as you can’t very well climb several trees at once). By default, this will be the output:

```
> climb tree
I don’t think much is to be achieved by that.
```

There’s nothing wrong with this output, except that it’s boring. We can make it more interesting using an Instead rule:

```inform7
Instead of climbing the tall old trees:
        say “Vicious flocks of sparrows and wrens dart down at you and peck at you with their sharp little beaks, driving you back.”
```

The actual result in the game is the same as before: Nothing has happened. The player is still standing in the room called Forest Path. (And if the player tries X SPARROWS, there won’t be any sparrows in the room. We haven’t yet created any!) But the game is a little more interesting and fun than before. As you write messages like this, you might even start to wonder, what are those sparrows and wrens trying so hard to protect? This might suggest a puzzle that you can add to the game, such as scattering birdseed to distract the homicidal songbirds. After scattering the birdseed, the player might be allowed to climb a tree after all. But that type of complication will have to wait for a later chapter.

> **Copying Example Code**
>
> As you read _The Inform 7 Handbook,_ you’ll find dozens of examples of game code that you can copy and paste directly into the Source page of the Inform program in order to try out the features that are illustrated in the code. These examples are all in codeblocks. If the examples contain indented lines, just copying and pasting them from the PDF _Handbook_ into your game may not work as expected. You can select the text of the examples and copy it, but when you paste the text into the Inform Source panel, all of the indentation will disappear, and extra carriage returns may have been inserted into long lines.
>
> Previous versions of Inform were entirely unable to understand code that didn’t have the correct indentation. The current compiler is much more forgiving, and will cheerfully process some material that has too many Tab characters at the beginnings of lines, or not enough of them. When you copy complex examples, however, it’s very possible that the compiler will get confused. To get the examples to work in Inform, you may need to eyeball them in your PDF reader, figure out where all of the indentations are (and exactly how many Tab keys each line is indented), and copy the indentations yourself manually, one line at a time. (See Chapter 8 of the _Handbook_ for more on indentation.)
>
>If you block-copy from the end of one page of the _Handbook_ onto the beginning of the next page, the page number will be copied along with the code. You’ll have to delete it in Inform.
>
>The _Handbook_ is also available online in the form of .odt (OpenOffice text) files. If you find yourself copying a lot of example code, it will probably be more convenient to download one of these files and use it as a source for copying.

### How Much Scenery Is Enough? {#how-much-scenery-is-enough}

As noted in Chapter 1, in the section “The Detail Trap,” it’s easy to get sidetracked by trying to cram too much scenery into a room. If your story is set in a modern house, the house will probably have a bathroom. You may be tempted to add a toilet, toilet paper, a sink with faucets, a bar of soap, towels and washcloths on a towel rack, a mirror that opens to reveal a medicine cabinet stocked with pill containers, a bathtub with a showerhead and a drain. This level of detail is probably not necessary, and may even be a bad thing. It’s a lot of extra work — and if you include these objects, the player will expect that manipulating them will have something to do with the story. If they’re just scenery, the player will be disappointed not to be able to look at herself in the mirror, turn the faucets on and off, and so forth.

All the same, it’s jarring, if the game includes a bathroom, to see this kind of output:

```
Bathroom
A typical bathroom. The door is to the west.

>x tub

You can't see any such thing.

>x sink

You can't see any such thing.

>x toilet

You can't see any such thing.
```

These responses destroy the illusion that the player is in a real room. A better approach is to create a single scenery object that stands in for all of the things in the room that aren’t important:

```inform7
Some fixtures are scenery in the Bathroom. Understand "sink", "toilet", "faucet", "mirror", "cabinet", "tub", "basin", "shower", "towel", "bath", and "mat" as the fixtures. The description is "The bathroom fixtures are not very interesting."

Instead of doing anything other than examining with the fixtures:

say "You have more important things to do right now than fiddle with the bathroom fixtures."
```

This preserves at least a thin illusion that the bathroom is a real place, while directing the player’s attention elsewhere.

Generally speaking, if an object is mentioned in the room description, it should probably be implemented as a separate scenery object. A “stand-in scenery object” like the one shown above would be a better choice for things that the player might naturally expect to be in this sort of room, but that aren’t important to the game.

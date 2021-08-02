## More About Room Descriptions

We’ve already seen (in the section on “Backdrops,” earlier in this chapter) a few examples of rooms whose description can change. These changes were produced by using square brackets to insert bits of code in the room description itself. This can be done with an if-test, as shown above in the example of the Throne Room, or with a [one of] insertion. There are other possibilities as well. These techniques are discussed in more detail in the section on “Text Insertions” in Chapter 9 of the _Handbook_, “Phrasing &amp; Punctuation,” but here’s an example of each technique to get you started:

```inform7
The Bog is south of the Desolate Moor. "The ground here is quite moist[if the fog is in the Bog], and the fog is thicker[otherwise]. A path extends out of the bog to the north[end if]."

The Sunlit Clearing is east of the Bog. "Sunlight streams down into this charming and cheerful space. [one of]Butterflies flit about you[or]A chipmunk scampers past[or]Songbirds twitter in the trees[at random]."
```

There’s more to room descriptions than this, however. Each time the player enters a new room or uses the LOOK action, Inform assembles a text to print out. The room’s name is the first part of this text; it’s followed by description you’ve written for the room. After printing out your room description, Inform will mention anything in the room that it considers interesting — mainly any visible objects that are not scenery.

The rules that are used for assembling the rest of the text are called the carry out looking rules. They’re complex, and this _Handbook_ is not the place to dissect them line by line. Instead, we’ll mention a few of the things that you may want to do to customize the appearance of your game. You may often want to control how various objects are listed as part of the complete room description. A large chunk of Chapter 18 of _Writing with Inform_, “Activities,” is devoted to this complex and useful topic, from 18.9, “Deciding the concealed possessions of something,” to 18.28, “Printing a locale paragraph about.” Close study of these pages and the Examples that go with them will give you plenty of ideas to experiment with.

Let’s look at a couple of ways to control the way objects are mentioned. We’ll start with this code:

```inform7
Use the serial comma.

The Living Room is a room. "Your comfy living room."

The paper clip is in the Living Room.

Buffy the Labrador retriever is a female animal in the Living Room.

The sugar candy doll house is in the Living Room.
```

The output reads like this:

```
Living Room
Your comfy living room.

You can see a paper clip, Buffy the Labrador retriever, and a sugar candy doll house here.
```

Notice that the list of items that Inform has constructed is in a separate paragraph. Also, notice that the items are listed in exactly the order they were mentioned in the source code. (The statement, “Use the serial comma,” puts a comma after the next-to-last item in the list.)

Now we’ll add one sentence to the code for Buffy. This sentence will be an **initial appearance**(explained more fully in Chapter 3). This new sentence, beginning “Buffy the Labrador retriever is lounging...”, is not a description. Only when we’re creating rooms and scenery can we write a description that doesn’t start with the phrase “The description is”. So Buffy has, as yet, no description; she only has an initial appearance:

```inform7
Buffy the Labrador retriever is a female animal in the Living Room. "Buffy the Labrador retriever is lounging here, shedding hair all over the place."
```

The initial description will remove Buffy from the list, and give her her own paragraph in the output. Now the output reads like this:

```
Living Room
Your comfy living room.

Buffy the Labrador retriever is lounging here, shedding hair all over the place.

You can also see a paper clip and a sugar candy doll house here.
```

Notice the word “also” in the last sentence. Inform has noticed that there was a separate paragraph about Buffy before the basic list, so it added an “also”.

Next, we’ll add a scenery supporter to the Living Room. (Containers and supporters are discussed in Chapter 3, “Things.”) Since it’s scenery, it won’t be mentioned as part of the list of objects in the complete room description, so we’ll want to add a bit to the room description property itself:

```inform7
The Living Room is a room. "Your comfy living room, complete with a falling-apart coffee table from Particle Board Heaven."

The coffee table is a scenery supporter in the Living Room. The description is "You really ought to replace it with something more upscale."
```

Adding the coffee table will have no effect on the way objects are listed in the room. But if we make one more change, we’ll see something new in the output. We’re going to put the paper clip on the coffee table:

```inform7
The paper clip is on the coffee table.
```

This changes the output significantly:

```
Living Room
Your comfy living room, complete with a falling-apart coffee table from Particle Board Heaven.

On the coffee table is a paper clip.

Buffy the Labrador retriever is lounging here, shedding hair all over the place.

You can also see a sugar candy doll house here.
```

This is Inform’s normal handling: A scenery supporter will be mentioned in its own paragraph, _but only if something is on it._ However, this is not true of scenery containers. The contents of a container are presumed to be less immediately visible than what’s on a supporter, so they won’t be mentioned unless the player actually looks in (searches) the container.

Mentioning the paper clip as shown above is probably just fine — there’s nothing very remarkable about a paper clip. But what if the object on the table is the priceless Etruscan figurine Mandy has been raving to you about throughout the first half of the game? In that case, this would be dull:

```
On the coffee table is an Etruscan figurine.
```

Eric Eve has suggested a simple way to get a more dramatic output, using the printing a locale paragraph about activity (see **p. 18.28** of _Writing with Inform_, “Printing a locale paragraph about”).

```inform7
Rule for printing a locale paragraph about the coffee table when the Etruscan figurine is on the coffee table and the number of things on the coffee table is 1:
        now the Etruscan figurine is mentioned;
        say "On the coffee table you espy the priceless Etruscan figurine Mandy has been raving about!";
        continue the activity.
```

Or perhaps you want that dramatic sentence to print only the first time the player enters the room rather than every time the figurine is still standing in solitary splendor on the coffee table. In that case, create a truth state (a true-false variable) that will shut off the special output after its first occurrence:

```inform7
Figurine-mentioned is a truth state that varies. Figurine-mentioned is false.
Rule for printing a locale paragraph about the coffee table when the Etruscan figurine is on the coffee table and figurine-mentioned is false:
        now the Etruscan figurine is mentioned;
        now figurine-mentioned is true;
        say "On the coffee table you espy the priceless Etruscan figurine Mandy has been raving about!";
        continue the activity.
```

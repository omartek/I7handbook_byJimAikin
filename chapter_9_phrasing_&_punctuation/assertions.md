## Assertions {#assertions}

As explained on p. 2.1 of _Writing with Inform_, “Creating the world,” an _assertion_ is a statement about something — usually about something in the model world you’re creating. A lot of your writing in Inform will consist of assertions. Here are some assertions:

```inform7
A saucer is on the table. The saucer is a supporter. A teacup is on the saucer.

North of the Sandy Beach is the Rocky Cove.

David is a man in the Living Room. David wears a leather vest and carries a walking stick.

Eye-color is a kind of value. A person has an eye-color. The eye-colors are blue, brown, and green.
```

The phrase “a kind of value” has a special meaning to Inform. We’ll discuss that in the section “Values,” below. The reason to include it here is so you’ll see that some assertions are a little more abstract than others — they may be about forms of computer data that Inform will need to know, rather than about physical objects in the model world.

The first thing to notice about assertions is that each assertion is a complete sentence. You don’t actually have to begin your sentences with capital letters — Inform doesn’t care about this. But it’s a good idea to get in the habit of writing Inform code so that it looks more or less like normal written English. (If you’re in the habit of texting in lower-case, using capitals may seem weird, but most forms of published writing require capitals.) An assertion can end either with a period or with a blank line of white space.

The second thing to notice is that the verbs in assertions are in present tense. (“Tense” is a term that refers to whether the action in the sentence takes place in the past, present, or future.) We can’t do this:

```inform7
David was a man in the Living Room. David wore a leather vest and carried a walking stick. [Errors!]
```

Those verbs are in past tense, and Inform won’t understand them. Your printed output can be in the past tense if you like, but that requires a bit of extra programming; for details, see [here](../chapter_10_advanced_topics/story_tense_and_viewpoint.md#story-tense-and-viewpoint) of the Handbook.

The third thing to notice is that when we’re writing assertions about physical objects, it’s a very good idea to start the sentence with “A,” “An,” or “The” in the normal way. (These words are called _articles._)With some types of phrases, Inform won’t care whether you use articles or not. But when you’re first creating an object, Inform will notice whether you use an article. It will also notice whether you begin the name of the object with a capital letter.

Here are three assertions that are very similar except for their use of articles and capital letters:

```inform7
The spoon is on the table.

Knife is on the table.

A Plate is on the table.
```

If we include these assertions in our game (after adding a table to the game, obviously), Inform will assume that Knife should always be capitalized and should never be given an article. That is, it will think Knife is a proper noun. It will assume that Plate should also be capitalized, but that an article should be used — because that’s what the assertions did. When the game gets around to constructing a list of the items on the table (Inform will do this automatically in certain situations), the game will print out the list like this:

```
On the table are a spoon, Knife, and a Plate.
```

This is ugly. But far from being a defect in Inform, this behavior is a strong point. If you read **p. 3.18** in _Writing with Inform_, “Articles and proper names,” you’ll see how easy it is to create objects whose names will be printed out in various sensible ways. The moral of the story is simple: Inform 7 can do almost anything that you might want it to do — but it’s up to you to think carefully about what you want it to do, and then use the correct syntax when writing your code.

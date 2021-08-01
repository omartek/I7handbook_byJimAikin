## Adding Vocabulary Words with “Understand” {#adding-vocabulary-words-with-understand}

When you create an object, such as the paintbrush we created earlier in this chapter, Inform is smart enough to understand two things at once. First: you, the author, can refer to the object in your code as a paintbrush, and the compiler will know what you mean. Second: the player who is playing your game can also call it a paintbrush, and the parser will know what the player means.

When you first start learning Inform, these two facts may seem to be almost the same — the object is a paintbrush, and that’s what it’s called. What could be complicated about that? But in reality, the name of an object for internal purposes (that is, when you’re writing code) is not at all the same thing as the word(s) the player can use to refer to the object or the words that are printed out by Inform as the story unfolds for the player. They’re often the same, but they don’t have to be. In fact, Inform allows you to make them completely different if you need to. (See the section on “The Names of Things” in Chapter 8 of the _Handbook_.)

After creating an object, you’ll almost always want to add extra vocabulary words to it — words that the player can use to refer to it. With a paintbrush, for instance, the player will quite often want to call it a brush. But the parser won’t understand that word unless you tell it to:

```inform7
The paintbrush is in the Tool Shed. Understand "brush" as the paintbrush.
```

Once you’ve added the second sentence, the player can use the word “brush” to refer to the paintbrush — but the author can’t. This is a key concept: The author can only refer to an object using the actual word or words that are used in the sentence that creates the object.

When you write a description for a new object, you’ll quite often find that you’re adding extra adjectives. These should always be added as vocabulary:

```inform7
The paintbrush is in the Tool Shed. The description is “The bristles of the paintbrush are stiff with dried paint.” Understand "brush", "bristles", "stiff", "dried", and "paint" as the paintbrush.
```

If you also have a can of paint in your game (which wouldn’t be surprising if you’ve created a paintbrush), the word “paint” will end up being ambiguous. It will be able to refer either to the brush or to the paint can (and possibly to the paint _in_ the can as well), and also to the command PAINT. Handling all of the possibilities in a case like this can get a little tricky. We’re not going to go through the whole troubleshooting process here, but it’s certainly something to be aware of when you start creating objects whose names and vocabulary words overlap.

Inform will attempt to keep track of what you mean when writing the game, and the parser will try to figure out what the player means when entering the word PAINT. If the parser can’t figure out what the player meant, it will ask questions. You can help the parser by writing “does the player mean” rules (see **p. 17.19** of _Writing with Inform_, “Does the player mean...”).

### Conditional Vocabulary {#conditional-vocabulary}

Most of the objects in a game will likely have the same vocabulary words from one end of the game to the other. But there are situations in which you may want to switch certain words on or off. For instance, if the vase gets broken during the game, the player should be able to refer to it as BROKEN VASE — but not otherwise.

The simplest way to do this is to refer to properties of the object when listing the vocabulary words:

```inform7
The porcelain vase is in the Museum Lobby. The vase can be broken or unbroken. Understand "broken" and "shattered" as the vase when the vase is broken.

Instead of attacking the vase:
        now the vase is broken;
        now the printed name of the vase is "broken porcelain vase";
        say "You shatter the vase."
```

Notice that the Instead rule both changes the broken/unbroken property of the vase and changes the vase’s printed name.

For more complex story situations, you may want to create scenes (as described in Chapter 8 of the _Handbook_) and make the vocabulary words that the player is allowed to use depend on whether a scene is happening:

```inform7
Daytime is a recurring scene. Daytime begins when the sun is part of the sky. Daytime ends when the sun is not part of the sky.

Understand "twittering" and "chirping" as the birds when daytime is happening.
```

For more on giving objects sets of words (like broken and unbroken) as properties, see the section on “Word Properties” later in this chapter.

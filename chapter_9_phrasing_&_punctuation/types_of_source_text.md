## Types of Source Text {#types-of-source-text}

There are three main kinds of writing in Inform. First, some of your writing will be between double quotation marks, “Like this.” There are two types of things that you put between quotation marks: what you want your game to print out to the computer screen (at some point or other) when the game is played, and words and phrases that you want Inform to understand when the player types them. Here’s a quick example that shows both of these types:

```inform7
The will is on the end table. The description is "A legal-looking piece of paper. You can't read what's on it, because it's upside down." Understand "legal", "legal-looking", "document", "paper", "piece", and "piece of" as the will.
```

The sentence following “The description is” is output text. This is what the Inform game interpreter will print out in response to EXAMINE THE WILL. The words after “Understand” are different: They’re extra vocabulary words for the object whose main name is “will”. The word “will” can be used both by the player of the game when referring to this object, and by the author. However, only the player can call it a “document” or a “piece of paper.”

The function of Understand rules is sometimes a bit difficult for new Inform authors to grasp, so let’s expand on the idea a bit. If you’ve used the code above to create an object called the will, you can _only_ refer to it in your source code as “the will” (or just “will”). You can’t write rules such as this:

```inform7
Instead of examining the legal document: [Error!]
```

Why not? Because the compiler doesn’t know that this object can be called “legal document.” In your source code, it’s important always to refer to an object using the word or words you used to create it. A little later in this chapter, we’ll look at a gray area that affects this concept, but it’s an important concept to get straight. If you forget what you called an object, you can even end up creating a second object with almost the same name, which can lead to hard-to-find bugs in your code.

The second type of thing you’ll write will be _comments_. Words and sentences that are _not_ between quotation marks but are instead surrounded by square brackets, [Like this], are comments. When your game is compiled, the comments will be ignored. Adding comments to your code is highly recommended! A comment is a memo you write to yourself, in order to take notes about things you still need to add to the story or so that you’ll remember, six months from now, why your code is constructed in a certain way.

As explained below in the section “Text Insertions,” however, square brackets have a completely different meaning when they’re _inside_ double-quotes.

Third, any writing that’s not between quotation marks and not surrounded by square brackets consists of instructions to the computer on how you want your game to operate — code, in other words.

With some minor exceptions, which we’ll get to below, Inform does not care what you put between quotation marks. You can write amazing poetry, if you feel up to it, and become known as a writer of rare gifts. Or you can spell words wrong, use clumsy grammar, and indulge in sloppy punctuation. In the latter case, the people who play your game may think you’re careless or badly educated, but these mistakes won’t matter to Inform. Inform won’t even notice them. It will just say, “Oh, that’s the text that I’m supposed to print out now.” No problem.

Text that’s neither a comment nor in quotes is a completely different matter. Inform will insist that you spell words correctly, that you follow certain rules for how phrases are worded, and that you use the right punctuation in every single line. Even a single mistake will stop Inform dead in its tracks. For instance, you might accidentally type a colon (:) instead of a semicolon (;) or vice-versa. This is easy to do, because they share a single computer key and look almost alike on the screen (especially when the screen is set to high resolution). But the colon and semicolon have completely different meanings to Inform. If you mix them up, when you click the Go! button to compile the game you’ll see nothing but Problem messages. You’ll find a list of a few common mistakes back in Chapter 1 of this book, [here](../chapter_1_getting_started/the_inform_7_program.md#the-go-button).

In this chapter we’ll look at the main rules you need to follow when writing your source code. It’s not easy to set out a complete set of rules for you to follow, because there are so many different things you may want to do while writing interactive fiction. Inform has lots of features, some of which require special types of syntax.

The I7 Documentation gives fairly complete explanations of the syntax, but it’s spread out in a lot of different places. Each type of syntax is discussed on the page where a feature that uses that syntax is introduced. In order to gather all of this information in one place, we’ll have to refer to some Inform features that you may not have run into. Don’t worry if you don’t understand every detail: This chapter is partly for you to refer to when you’re trying to figure out why Inform doesn’t want to compile your game.

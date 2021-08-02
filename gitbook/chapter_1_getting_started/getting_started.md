# Chapter 1: Getting Started

![](../assets/graphics19.jpg)

So … you’d like to try writing interactive fiction. It looks like fun, but you’re not sure where to start. Or maybe you’ve already started, and now you’re getting confused, or you’re not sure how to get the results you want.

This book will help you make sense of it all. Every chapter (except the last one, which is sort of a grab bag) is about one specific part of the writing process.

You don’t need to read the book straight through from top to bottom. Feel free to jump around, dipping into whatever chapter looks as if it will have the information you need. If you want to write a story with lots of characters, for instance, you may want to head straight to Chapter 5\. If you find that you’re having trouble writing things in a way that Inform understands, you can consult the tips on phrasing and punctuation in Chapter 9\. Some of the discussion in that chapter is pretty deep, though, so it may not be the best place to start learning. (That’s why it’s Chapter 9, not Chapter 1.)

Even right here in Chapter 1, there are things you won’t need to think about yet when you’re just starting out. If you hit something that doesn’t make sense, feel free to skip it and come back to it later.

Unlike a technical document, which attempts to lay out the features of a system in an orderly manner, explaining the most basic concepts first in order to build on them later, the _Inform Handbook_ is organized in a way that attempts to get you started doing useful and interesting things quickly. To be sure, the opening chapters cover the basics and contain many cross-references to concepts that will be explained later. Nonetheless, as early as Chapter 2 you’ll find things like text substitutions and before, after, and instead rules used in the example code with no real explanation of what they are or how they work. When you encounter something in an example that is unfamiliar, you can safely assume not only that it works, but that it will be explained in a later chapter.

Whether you read this book or some other manual, or just dive in and start trying things without bothering to read a manual at all, you’ll soon learn that writing interactive fiction (“IF” for short) is more than just creative writing. Creativity and storytelling are definitely part of the process, but you’ll also be doing a type of _computer programming_. “Programming” means you’re giving the computer instructions about what to do. And computers are incredibly picky about understanding your instructions! As you start writing IF, you’ll find that a single misspelled word or a missing period at the end of a sentence can stop the computer dead in its tracks. Later in this chapter I’ll give you a short list of mistakes that I’ve seen students make.

This book is about how to use the popular Inform 7 programming language (“I7” for short). There are several other languages in which you can write interactive fiction, as mentioned in the Foreword. If you’re using one of them, you’ll find a few general tips in this book that you can use. In particular, the discussion of puzzles in Chapter 6 is largely platform-independent. Nonetheless, the book is mostly about how to use I7.

I feel Inform 7 is an especially good choice for those who are new to writing IF and also new to computer programming. I7 is designed to make it as easy as possible to get started. The computer code you’ll be writing looks very much like plain English, because (barring a few oddities) it _is_ plain English. Having said that, it has to be admitted that the I7 application (in which you’ll be writing your game) has a number of facets, which can make it seem intimidatingly complex.

Certain features that experienced may expect, such as single-step debugging, are not possible with I7\. Even so, I7 includes many “power user” features for game design, so it won’t limit you if you want your story to include complex things.

As a _caveat,_ however, I should add that if you’re thinking you’ll dip your toes in the ocean of computer programming by writing some interactive fiction and then later consider moving on to a general-purpose language like Javascript or C++, Inform 7 would be a poor choice. Its syntax is quite unlike what you’ll find in most programming languages, and the programming skills you learn by writing stories in I7 will be difficult to translate into a form you can use in any other programming language.


> **Is It a Game, or Is It a Story?**
>
>In _The Inform 7 Handbook_, we’ll refer to an Inform project as either a “story” or a “game,” without making much of a distinction between the two words. There are some real differences: Some interactive fiction has a strong story and very little in the way of game-type fun. Other interactive fiction is mainly a game, and the story is so weak it might as well not exist at all.
>
>It’s up to you to decide how to combine story elements with game elements. For the purposes of this book, the game is a story and the story is a game. In recent years the designers of Inform have been leaning toward “story” as a term for what you’ll be producing, but I still prefer to think of it as a game.
>
Inform 7 is the successor to Inform 6, which is also a popular language for writing IF. The two are completely different, even though they were created by the same person, Graham Nelson, and are both called “Inform.” In this book, we’ll most often refer to “Inform” and not bother to add the 7, but all of these references are to Inform 7, not to Inform 6.

It’s important to note that Inform 7 is still being developed. The most recent version at this writing (spring 2015) is version 6L38\. It and its immediate predecessor, 6L02, are significantly different from earlier versions. People have been using I7 successfully to write interactive fiction for close to ten years, but like most other programming languages, it isn’t officially finished, and may never be. If certain of the details in this book don’t seem correct when you try them out, it’s possible that you’re using an earlier or later version of Inform, in which the features are different. The basic I7 language is pretty well developed, and probably won’t change too drastically in the future, but the recent refinements are significant.

In addition to possible changes in the language, the numbering of pages and Examples in Inform’s built-in Documentation is quite likely to change. Please note that all of the page and Example numbers given in the _Handbook_ refer to version 6L38.

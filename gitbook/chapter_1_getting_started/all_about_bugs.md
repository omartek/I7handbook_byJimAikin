## All About Bugs

![](../assets/graphics6.png)

When a computer program doesn’t do what it’s supposed to do, it either does the wrong thing or, worse, stops working entirely. This type of problem is referred to as a _bug_. According to legend, one day the scientists who were trying to use one of the very earliest computers kept getting mysterious errors. After hours of frustration, somebody thought of opening the box of circuits and looking inside. A dead moth was lying on a circuit board, making an electrical connection where no connection was supposed to be. After that, the scientists started saying that any mysterious behavior in their programs was caused by “a bug.”

![](../assets/graphics42.jpg)

Finding and fixing bugs is a huge part of computer programming. Fortunately, most of the bugs you’ll run into don’t involve dead insects! (Although that might make an interesting puzzle....) Most bugs today are caused by errors in the instructions (the source code) that the computer is trying to run.

We all write source code that has bugs, so you may as well get used to it. Most bugs are easily found and easily fixed. A few of them may drive you crazy for hours at a time. It’s all part of the process.

Inform bugs come in four different varieties.

![](../assets/graphics41.jpg)

When you click the Go! button to tell Inform to compile your source code into a game, the compiler may encounter errors. You may have written things that Inform doesn’t understand. Instead of producing a game, Inform will print out an error message, or a bunch of them. Usually these messages will give you a pretty good idea what you need to fix — but sometimes the compiler can’t quite guess what the real problem is, so you may need to try a bunch of changes until you find something that works.

In the second type of bug, when you click the Go! button, your game may compile successfully and appear in the right-hand window, ready for you to try out. But the game may not behave in the way you expect. An object that you meant to put in plain sight in a room might not be anywhere in the game, for example. Inform can’t find these bugs for you. The only way to find them is by testing and retesting your game while writing it. Try out a bunch of different commands, including silly ones, just to see what happens. (This is called “trying to break it.”)

The third type of bug is called a “run-time error.” In a run-time error, your game tries to do something that it can’t do. Instead of producing some type of normal output, the game will produce an error message. Run-time errors can happen, for instance, when your code tries to refer to an object that doesn’t happen to exist. When you run into a run-time error, look closely at the error message in the game panel, and then at the code that is being used by the command that triggered the error.

![](../assets/graphics43.jpg)

The biggest run-time errors are those that cause the game to freeze or quit unexpectedly. Fortunately, these are fairly rare. But don’t be surprised if it happens — just go back to the code that was being run in response to your last command. Nine times out of ten, that’s where the problem will be found.

If you’re having trouble finding a bug, a useful technique is to “comment out” a section of your source code that you think might be causing the problem. In Inform, comments are surrounded by square brackets [like this]. Any text that is within square brackets will be ignored by the compiler — unless it’s within double-quotes. Within quotes, square brackets have a different purpose, as explained in the “Text Insertions” section in Chapter 9, [here](../chapter_9_phrasing_&_punctuation/text_insertions.md#text-insertions).

By commenting out blocks of code, you can test a game both with and without selected features. This will help isolate a trouble spot.

The fourth type of bug can look like any of the first three. Because Inform itself is still being developed, the compiler undoubtedly has a few bugs of its own. If you encounter something weird when you seem to be doing everything right, it could be a compiler bug. 97% of the time it won’t be — it will be your code. But compiler bugs do exist. If you should run into something that looks like a compiler bug, your first step should to post a message to the intfiction.org forum asking for confirmation of what you’ve found. If it is indeed a compiler bug, you’ll want to file a bug report. The Inform website (http://inform7.com/support/) has instructions on how to do this. There is also a bug tracker website (http://inform7.com/mantis/my_view_page.php) where you can check whether a given bug has already been filed. If not, you can file a report and keep an eye on it. You can also check here to discover what other bugs you’ll need to be aware of while writing. Most of them are relatively obscure and shouldn’t cause you any trouble, but some are worth knowing about.

## Headings

Another difference between Inform and traditional programming languages is that, with some important exceptions, Inform doesn’t care where you place rules and assertions. If you want to mix up your source code, leaving related bits strewn out all over everywhere, Inform will let you. If you’re working on the section of the story that has to do with the swords, and you suddenly realize that you need to make sure the men in the tower are wearing chain mail, you can just hit a couple of Returns to start a new paragraph and create the chain mail on the spot. There’s no need to go find the men in the tower (they could be five hundred lines earlier or later in the file) and put the chain mail in their part of the code.

This is bad programming practice, though. It’s much better to keep related code together. Inform’s Index World tab will help you find everything in your code, no matter where it is. But if you create your own organization, the writing will go more smoothly, and you’ll end up with fewer bugs.

The natural and normal way to do this is by writing headings, as explained on **p. 2.5** of _Writing with Inform,_ and putting all of the code for some specific thing below a single heading. For instance, the chapter on the wizard might include a section called “Conversations with the Wizard.”

The larger your game is, the more important it will become to use headings in this manner. In most programming languages, you can put various parts of the code in separate files on your hard drive. Inform doesn’t allow this, because it’s designed around the idea that what you’re writing is a story or book, which would naturally be one continuous block of text.

Using headings within a single file is almost as convenient as organizing your program in multiple files, and it has some advantages too. After you’ve compiled your game, the Index Contents tab will display an outline of the source code, listing all of the headings. There’s also a Contents tab in the Source pane. This makes it easy to move around in a large file — just click on the heading, and the Source pane will jump to it. (If you’ve added code since the last time you compiled, this mechanism may not work perfectly. Click the Go! button and then look at the Contents page of the Index again.)

How you organize the code and give headings to the various sections is almost entirely up to you. The only requirement is that each heading be on a line by itself, with a blank line before it and another blank line after it.

Inform recognizes five words as headings: volume, book, part, chapter, and section. When the Index is being constructed, these five headings are considered _hierarchical_, which is just a fancy way of saying that a volume is bigger than a book, a book is bigger than a part, and so on. But you can ignore the hierarchy if you like, and give sections headings in whatever order you like. A well organized outline might look like this:

Volume 1 – The Castle
        Book 1 – The Courtyard
                Part 1 – The Courtyard Room Itself
                Part 2 – Scenery in the Courtyard
                Part 3 – The Guard
                        Chapter 1 – The Guard Himself
                        Chapter 2 – Conversations with the Guard
                        Chapter 3 – Being Chased by the Guard
        Book 2 – The Dining Hall

...and so on.

Many Inform programmers prefer to number their volumes, books, parts, and so on, as shown above. But the numbers don’t have to be in order, and numbering is not even required. All that’s required is that there be _something_ after the heading word. If you just type Chapter and then forget to put anything after it, the compiler will complain. (Also, you can’t put a period or colon immediately after a heading word.)

Giving each heading a name is a very good idea. This will help you understand what you’re seeing in the Index.

One of my students put a bunch of related material in a single chapter and then asked, “How can I tell Inform, ‘Chapter 3 starts now’?” This is a very reasonable question, but the answer is — you can’t. The headings are strictly a way to organize your source code. They have no effect whatever on what happens when the game is being played. To switch to a new set of circumstances at a certain point in the game, you need to use scenes, as explained in Chapter 8 of this _Handbook_ and **Chapter 10** of _Writing with Inform_, “Scenes.”

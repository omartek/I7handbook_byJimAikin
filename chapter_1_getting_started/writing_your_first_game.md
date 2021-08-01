## Writing Your First Game {#writing-your-first-game}

There are no rules at all that dictate what you can put in a game. One of the great things about interactive fiction is that you’re free to write whatever sort of story you’d like, and put whatever story elements in it you think would be fun.

Your first game may be just something that you put together for fun, or as a surprise for your kids. But if you hope to create a game that you can share with other people, you may want to think carefully about what people will be able to see and do when they play your game. Here are a few tips that may help you come up with a better game. If these tips don’t make sense now, come back to the list in a few weeks — it may make more sense after you’ve done some writing.

1.  Players won’t be able to read your mind. If you want them to know about something (such as which directions they can go when they’re in a certain room, or the fact that a time bomb is ticking), you need to write some output text that will tell them. Output text is the material that appears in double quotation marks within your source text.

2.  When creating objects, always add all of the vocabulary words you can think of that players might use to refer to the objects. (See “Adding Vocabulary Words” in Chapter 3, [here](../chapter_3_things/adding_vocabulary_words_with_understand.md#adding_vocabulary_words_with_understand), to learn how to do this.)

3.  When creating new actions that will work on your objects, always add all of the verb synonyms you can think of. Forcing the player to guess what verb you had in mind is considered extremely poor form. (The techniques for creating new actions are explained in Chapter 4, starting [here](../chapter_4_actions/creating_new_actions.md/#creating_new_actions).)

4.  After writing a few paragraphs, click the Go button to compile your game and test your work. Test all of the silly commands you can think of, and watch how your game handles the commands. Then rewrite and test some more. Don’t wait until you’ve written great swaths of source text before compiling; failing to compile often is just a way to give yourself lots of needless headaches.

5.  Write an intro to your game (using a When Play Begins rule — see Chapter 8 [here](../chapter_8_time_&_scenes/passing_time.md#passing_time)) that gives players a clear idea about two or three things: Where the story takes place, what character they’re supposed to be, and what that character is trying to do.

6.  If you plan to have anyone outside your immediate circle of family and friends play the game, you’ll want to enlist at least two beta-testers, as described [here](./testing_your_game.md#testing_your_game).

Even before you write the first sentence of your story, Inform contains a great mass of rules that will allow your game to do some sophisticated things automatically. The game can, for instance, construct sentences that you never wrote, in order to describe situations that may come up during the story. The rules that are included in I7 are called the **Standard Rules**.You can use them without knowing anything about them. In fact, you will be using them in every game, unless you explicitly switch some of them off. Just about every rule in the library can be individually disabled (switched off) if it produces results that you don’t want. Switching off portions of the library is an advanced programming topic, but the basic technique is illustrated [here](../appendix_b_updating_older_extensions.md#new-rule).

If you’re curious about what the Standard Rules look like, you can open them from the Inform IDE. In the Macintosh, choose File &gt; Open Extension &gt; Graham Nelson &gt; Standard Rules.

Please be careful not to make any changes in this file! If you do accidentally make changes, be sure to close the file without saving. Changing the Standard Rules could mess up Inform so that the games you write won’t work properly, or at all. (If this happens, you can always download and reinstall Inform. Reinstalling will not affect the game you’re working on.)

### From the Top {#from-the-top}

To start your game, you need to create at least one room, where the story will start. Chapter 2 of this book is all about how to create rooms. Before you start writing your first room, though, you may want to do a couple of preliminary things. I recommend starting your game as shown below. First, the game should have a title and a byline. (These will be created automatically by Inform when you start a new project, but you can change them at any time just by editing the first line in the Source page.) After the title and byline, skip a line and write a Use sentence, like this:

```inform7
Use American dialect and the serial comma.
```

Inform was written by an Englishman, so it uses British spellings for a few words unless you instruct otherwise. “Use American dialect” switches the spelling from British to American. If you want the game to start out in brief mode, do it this way:

```inform7
Use American dialect, brief room descriptions, and the serial comma.
```

Prior to version 6E59, Inform’s default for room descriptions was brief mode, but the default has been changed to verbose mode. Here’s the difference: When the game is in verbose mode, the player will read the complete description of each room each time she enters the room. If the game is in brief mode, the room description will be printed out in full only the first time the player enters a room; after that, the room name will be printed more or less by itself. (Any movable objects or people in the room will still be mentioned.) The player can switch full-length room descriptions on and off using the VERBOSE and BRIEF commands, which are built into Inform, so telling Inform that you want to use brief room descriptions only controls how your game will start out, not what may happen after that. If the solution of a puzzle relies on the game being in verbose mode, but the player has switched to brief mode, you’ve written an unfair puzzle! (Here’s a **bonus tip**: If the room description has changed as a result of some action the player has taken, and you want to make sure the player sees the new description, make the room _unvisited_ when the player takes that action. For more on how to do this, see “When Is a Room ‘Visited’?” [here](../chapter_2_rooms_&_scenery/when_is_a_room_visited.md#when-is-a-room-visited).)

The serial comma is the final comma in lists of items. If the serial comma is switched on, your game might report this:

``You can see an apple, a pear, and a banana here.``

If the serial comma is _not_ being used, the output is just slightly different:

``You can see an apple, a pear and a banana here.``

Most games also need an introduction — some text that will “set the stage” for the story. You can create an introduction by writing a When Play Begins rule, perhaps something like this:

```inform7
When play begins, say "Lord Triffid has invited you to spend your week's vacation in his castle. Upon arriving, though, you begin to feel a bit uneasy. Perhaps it's the bats flying in and out of the attic window that put a damper on your mood, or perhaps it’s the sound of barking, snarling guard dogs...."
```


### The Detail Trap {#the-detail-trap}

When writing your first interactive fiction, there’s a pitfall you may want to watch out for — the detail trap. Let’s suppose you want your story to start in the kitchen of the main character’s house. So you start putting things in the kitchen — appliances and so on. (By the way, **p. 8.5** of the _Recipe Book_, “Kitchen and Bathroom,” has some great tips on how to make appliances.) Now, a kitchen is a complicated place! The stove can be switched on, and touching it when it’s switched on will burn you. The hot and cold water taps in the sink can also be turned on, and when one of them is on, there’s some water that the player might want to interact with. In the refrigerator is some moldy cheese, so you need to figure out how Inform handles the smelling action.

And so on. Two months later, you’re still trying to work out the details of a realistic kitchen. (What if the glass in the cupboard is half-full of water instead of completely full? If you empty a half-full glass on the floor will it only make a small puddle instead of a large puddle?) Meanwhile, your story has gone nowhere, and your enthusiasm for interactive fiction has taken a nosedive. That’s the detail trap.

A better approach, I’ve found, is to start by creating a bunch of rooms and putting perhaps a couple of major scenery items in each room. (Scenery is discussed in Chapter 2.) Then create a few simple puzzles. Then add one or two important characters — but only in a basic way. Don’t worry about the nuances of conversation yet. (Characters and conversation are covered in Chapter 5.)

I like to write descriptions when I’m starting out, because I like to get a concrete feeling for the places and objects in the story. To start with, though, write basic descriptions of rooms and important objects without worrying about how the objects may change during the course of the game. You can always edit the descriptions later to allow them to change dynamically, or to take account of details that are added to the code later.

There’s a lot to learn in Inform. So start with simple things and build up your game in an orderly way. Put off the complex and tricky stuff for a later stage in the development.

### Title Trickery {#title-trickery}

We’re going to take a little detour into more sophisticated Inform programming here — nothing that’s tricky to write or understand, but we’ll use a couple of Inform’s deeper features without bothering to explain them. The reason we’re going to do it here is because of what happens at the very beginning of the game.

After your intro, Inform will print the banner text. (Don’t confuse the banner text, which is printed only once, with the status line, which looks like a banner and usually runs across the top of the interpreter window throughout the game.) If you’ve given your game a title and subtitle, they’ll appear in the banner text, which might look something like this:

```inform7
A Screw Loose

A Digital Dalliance by Jim Aikin

Release 1 / Serial number 150215 / Inform 7 build 6L38 (I6/v6.33 lib 6/12N) SD
```

Wondering how to put a cool subhead underneath the game’s title, like the one shown above? That text is called the story headline. You do it like this:

```inform7
The story headline is "Digital Dalliance".
```

Providing the release number, serial number, and so on as part of the banner is not anything you need to set up; it’s done automatically, as a courtesy to players. Among other things, it will help you keep track of different versions of your game, if you release more than one version. But there may be games in which displaying this text is not desirable. You may want to replace the default banner text with your own text, or suppress it entirely. To do this, you could add code like this near the top of your game:

```inform7
Rule for printing the banner text: say "[bold type]I'm a lumberjack and I'm okay![roman type][line break][line break]"
```

Whatever you write as a rule for printing the banner text will be printed out as the banner. Instead of using a “say” phrase as shown above, you can write “do nothing” here, which will suppress the banner text entirely. If you’re replacing the banner text, you might want to include your own version number. (Inform’s version numbering doesn’t allow decimal points, which makes it a bit nonstandard in the computer world, so writing a banner text such as “A Screw Loose, version 1.01” might be worth considering.)

Writing a new rule for printing the banner text, however, will _also_ change the banner text information when the player types the VERSION command. The release number, serial number, build number, and compiler number will be unavailable. This is less desirable. If you want to suppress the banner text at the beginning of the game but keep the information available in response to the VERSION command, you can do it this way:

```inform7
The display banner rule is not listed in the startup rulebook.
```

This will eliminate the opening banner but leave the version information intact, so the player will be able to display it with the VERSION command. Substituting your own banner text when play begins while keeping the existing text in response to the VERSION command is possible but tricky, so we won’t get into it here.

Before we move on, we need to pause for a quick cautionary note: The title of an Inform game can’t contain quotation marks. That is, if you want your story’s title to be displayed this way:

``“Repent,” Said the Tick-Tock Man``

… you just plain can’t. You can, however, use single quotes (apostrophes), producing this title:

``‘Repent,’ Said the Tick-Tock Man``

A problem that used to crop up more often has now been fixed. In some previous versions of I7, it was impossible to use an apostrophe in the title if the apostrophe fell at the end of a word. That is, you couldn’t call your story “Goin’ Home”. This is now allowed. You can just type an apostrophe at any point in the title, either in the middle of a word or at the end, and it will be displayed properly.

### Telling a Story {#telling-a-story}

Maybe the most basic way to look at a story — any story, be it interactive, written on paper, or told out loud — is that a story is about a person who has a _problem_. The reason for looking at stories this way is simple: If the main character in the story doesn’t have a problem, the story will be extremely boring. When we read a story, we want to enjoy the suspense of wondering how the lead character will solve the problem, and then at the end we want the satisfaction of seeing how the problem was resolved. In interactive fiction, the player usually _is_ the lead character, which can add to the suspenseful emotions your reader/players will feel.

The problem in a story can be as small as finding a lost kitten, or as large as saving Earth from alien invaders. As long as the problem is emotionally important to the lead character, it will work in a story.

If the problem is too easily solved, the reader (or player) will feel cheated. So the author needs to make sure the problem is not only important to the character, but not too easy.

In interactive fiction, solving the main story problem usually means solving a variety of puzzles. This _Handbook_ has a whole chapter (Chapter 6) on designing puzzles.

> **What’s a WIP?**
>
> As you read discussion of interactive fiction programming in Internet forums and newsgroups, you’ll often find somebody talking about “my WIP.” This is an abbreviation for “work in progress.” Large games can be “in progress” for months or years. As long as you’re still working on an unfinished game, or even thinking about it once in a while, it’s a WIP.

### Managing Your Project(s) {#managing-your-project-s}

It’s a good idea to always save your project to some specific folder on your hard drive. In Windows, this would probably be My Documents &gt; Inform &gt; Projects. If you care about your creative work (and you should!), it’s a very good idea to _back up_ your project to a separate location after you’ve done any new work on it. USB memory sticks are cheap and convenient. Always use a separate _physical_ location for backup, not just a different partition on the same physical hard drive. The point of making a backup copy is to protect you against the possibility of a hard drive crash or system failure.

Every few days, I like to save a project using a new, numbered filename. After working on Flustered Duck 05 for a few days, I’ll use the Save As command and save the project as Flustered Duck 06, and so on. (The final release version of “A Flustered Duck” was project version 21). Here’s why that’s a good idea: If you should change your mind about a design decision that you’ve made, or if you should accidentally delete or change something without meaning to, you can open up an older version of your project and copy a portion of the source code from the old version into the new one. Doing this actually saved me from a serious problem when I was writing this _Handbook._ I recommend it highly.

### About Inform Source Code {#about-inform-source-code}

One of the strong attractions of Inform 7 for new authors who would like to try writing IF is its use of natural language syntax. In many simple situations, both writing Inform source code and reading it is easier than wrapping your brains around a more conventionally structured programming language (such as TADS 3 or Javascript). Unfortunately, there’s a downside to this apparent ease of use, which will become more apparent as you get deeper into writing your game. Inform’s programming language contains a lot of one-off syntax — phrases that make sense if you know them, but that are hard to guess if you don’t know them. If you can’t remember how a given line should be written, your game probably won’t compile, and the compiler’s error message may not be very helpful. And if you can’t remember the phrase to use, searching the Documentation for it may not work either.

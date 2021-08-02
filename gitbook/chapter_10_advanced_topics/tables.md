## Tables

Tables are Inform’s way of organizing complicated blocks of data. **Chapter 16** of _Writing with Inform_, “Tables,” will tell you a great deal about tables, but it won’t, at first glance, give you a very clear idea why you might want to use a table. I’m pretty sure you can write a complete and satisfying game without ever using tables. They’re a specialized tool, used mainly when you have long lists of stuff that you want to be able to organize and then get at during the game. Tables are used in creating hint menus and conversation menus, for instance.

When I asked the Inform experts for ideas about why an author might want to use a table, Emily Short provided an excellent list. I’ll include her suggestions here, with only minor editing, in case they might give you an idea or two for your next game.

>**Emily Short on Using Tables**
>
>The most common uses for me are these:
>
>— To manage background-event text. This might take the form of events that need to happen in sequence, during a scene (see “Day One”), or it might be a set of randomized atmosphere texts to be printed under certain conditions. I use this trick _all the time_.
>
>— To store the mental equivalent of inventory. In my story “Alabaster,” for instance, there is a long, long list of facts the player might know, each of which has a short summary text to be printed by THINK if the player has in fact discovered this fact. This information is stored like this:
>
>```
>Table of All Known Facts
>fact                 summary
>snowshoes-worn       "She is wearing snow shoes."
>apple-pie            "She really likes apple pie."
>```
>...and so on, for dozens of lines. (Actual facts changed to protect against spoilers.)
>
>— To give an NPC pert replies to being asked to do dumb things. I find it most convenient to make a table of the different rules that cause an action to fail, and then attach some reply text to each one. (Example 188, “Generation X,” demonstrates this.) I could also handle this with a series of individual “unsuccessful attempt” rules, but because there would have to be a large number of these, I find the table is easier to take in at a glance.
>
>— To construct any kind of consultable object in which the player needs to look things up: books, computers on which you conduct Google-style searches, or the sort of NPC that exists chiefly to answer questions. (Most of mine don’t, which is why I usually don’t use tables to construct them; but I could imagine a robot librarian that would be best implemented by a table.) Several reviewers commented favorably on the computer database search in “Floatpoint,” and this would have been vastly harder to set up without tables with topic columns.
>
>— To store flexible schedules. Inform has various time functions that make it possible to write an inflexible schedule (X happens at a given time of day, no matter what), but sometimes I like to have a free-floating schedule that could start at any time. My extension “Transit System” is a good example of this in action: Each row contains a number of minutes and the name of a room, which is the stop where the bus (say) ought to arrive after the requisite delay.
>
>There are also some obscure programmatic uses to them, of which the most obvious is perhaps:
>
>— As an aid in extensions, whenever I want to create a sequence of things to which the author of the game may need to add. Because tables can very easily be amended or added to, they make good structures for an extension designer to use. “Complex Listing” exemplifies this: It offer several kinds of list-building options but allows the game author to add almost any kind of addition to the selection.
>
>In practice, the things you can do with a table are not _that_ numerous. They basically boil down to:
>
>To find your place in a table, you can step through the whole table row by row. You can choose a specific row, by row number or by looking for a specific value in one of the columns, or by selecting a blank row with nothing in it yet.
>
>Manipulating the contents of a particular row, once chosen: You can read and use a table entry for something (for instance, to print text or set a local variable). You can write something new in a table entry. Or you can blank out a row of entries, eliminating them permanently.
>
>You can manipulate the whole table by sorting the table to put one of the columns in a specific order.
>
>Even topic tables are just a special case of this, in that they have a column with a special name (“topic”) and they allow the author some shorthand for looking up rows in the table based on the player’s input — but this is still just row-choosing stuff.

In a nutshell, here’s what you need to know about tables in order to start using them:

The data in tables is organized into rows and columns. Each column has a name, which is how you’ll refer to it while writing your game. The table itself has a name too. The rows don’t have names; they’re numbered. That is, they’re implicitly numbered — when you write out your table, you don’t use numbers.

Each column can contain only one type of data. The first column might contain things, for example, the second column numbers, and the third and fourth columns text. If you try to mix up the columns, for instance putting a number where text belongs, Inform won’t let you. An entry in any row or column can be left blank by typing two hyphens (--).

When you create a table, you separate the data within each row by using one or more Tab characters. Rows of space characters look the same to you and me, but they won’t do the job. At the end of each column, you hit a single Return/Enter, and then start the next column. Tables with long texts tend to look quite jumbled on the Source page, but if you follow these rules and ignore how the table looks on the screen, it will work the way you want it to.

Let’s create a table, so that we can refer to it in the rest of this section:

```inform7
A furry menace is a kind of thing.

The gopher is a furry menace in the Meadow.
The muskrat is a furry menace in the Meadow.
The chipmunk is a furry menace in the Meadow.
The mole is a furry menace in the Meadow.

Table of Obnoxious Mammals
critter       name          weight
gopher        "Herman"      17
muskrat       "Vivian"      12
chipmunk      "Abercrombie" 9
mole          "Edith"       27
```

The first row under the table name contains the column headings (critter, name, weight). These are just abstract words, as far as Inform is concerned. I’d recommend not using a word that Inform is using for something else, or that you’re using elsewhere in your own code. You should avoid column headings like “location” and “container”, for instance.

To use the data in any cell in the table, we can refer to it by the line number and column heading. For instance, “the name in row 4 of the Table of Obnoxious Mammals” is the text “Edith”. If you’re familiar with computer programming, you’ll understand when I say that Inform’s table rows are 1-indexed, not 0-indexed. In plain English, the number of the first row is 1, not 0.

You can also get at the data in the table by cross-referencing the data you want with the data in some other column, like this:

```inform7
say "The name of the muskrat in the Table of Obnoxious Mammals is [name corresponding to the critter of muskrat in the Table of Obnoxious Mammals]."
```

Note the slightly weird syntax here. We have to say “corresponding to the critter of muskrat” — we can’t say, “corresponding to the muskrat critter.”

You may sometimes need to change the data in a table during the course of the game. Inform’s standard “now … is” syntax will do the job:

```inform7
now the weight in row 1 of the Table of Obnoxious Mammals is 8;
```

It’s often useful to look at all of the data in a table, one row at a time. Here’s one way to do that:

```inform7
repeat with N running from 1 to the number of rows in the Table of Obnoxious Mammals:
        if the weight in row N of the Table of Obnoxious Mammals is greater than 15:
                say "[Name in row N of the Table of Obnoxious Mammals] is rather obese."
```

The phrase “repeat with N running from 1 to the number of Rows in the Table of Mammals” is explained on **p. 16.6** of _Writing with Inform._ This phrase has several elements. The phrase “repeat with” creates a _loop._ Inform will run through the code block below the “repeat with” statement over and over. The first time through the loop, N will be 1\. The second time through the loop, N will be 2\. And so forth. N is a _loop counter;_ the words “running from 1 to” are what tells Inform that N is a number, and that it’s a loop counter. The phrase “the number of rows in the Table of Mammals” should be obvious; in this case it’s 4, because our silly little table has four rows. So the loop will run four times, and then stop.

While the loop is running, we can use the number N (which is different each time Inform goes through the loop) to do various things to the data in the table. Mainly, we can look up data in row N, or we can change it.

Here’s a more concise way of doing the same thing, without using a loop counter:

```inform7
repeat through the Table of Obnoxious Mammals:
        if the weight entry is greater than 15:
                say "[name entry] is rather obese."
```

As mentioned on **p. 16.12** of _Writing with Inform_, “Listed in...,” when Inform looks at some data in a table row, that row is automatically chosen. This makes it easy to refer to the other data in the same row without having to tell the compiler what row we’re talking about. Here’s an example that shows how this works. Because we defined the objects that show up in the table as of the furry menace kind, we can write a rule that will apply to any furry menace:

```inform7
Instead of examining a furry menace (called FM):
        if FM is a critter listed in the Table of Obnoxious Mammals:
                say "[The FM] is named [name entry]."
```

We don’t need to say “[name corresponding to the FM in the Table of Obnoxious Mammals]” — in fact, we can’t say it, because Inform won’t know what it means. Because the row has already been chosen automatically, “[name entry]” will work fine.

Sometimes you may need to change the data in a table entry. You can do this by referring to an entry in another column of that same row, which is convenient, because it means you don’t need to know the number of the row the data is in. Continuing with our rather silly example, we’re going to create a new action, altering, which will do nothing except change the entry in the name column:

```inform7
Altering is an action applying to one thing. Understand "alter [furry menace]" as altering.

Carry out altering:
        now the name corresponding to a critter of the noun in the Table of Obnoxious Mammals is "Judy Garland";
        say "Name altered."
```

The point of this example is to show the syntax. Two of the columns are called name and critter, so “now the name corresponding to a critter of the noun...” will let us alter the name of any of the critters to “Judy Garland” by typing ALTER MOLE in the game, or ALTER MUSKRAT.

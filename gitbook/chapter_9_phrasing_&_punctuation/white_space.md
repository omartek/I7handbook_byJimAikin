## White Space {#white-space}

When you’re writing a game in Inform, does white space in your code matter? Sometimes yes, sometimes no. Because Inform is designed to look like “natural language,” its use of white space is a little trickier than in some other programming languages.

Places where white space matters include around headings (see “Headings,” later in this chapter) and when you’re using Tab characters to organize tables and logical blocks of code (see “Indentation”).

Each heading must have a blank line before it and a blank line after it. The line containing the story title and byline (on the first line of the Source file) must also have a blank line after it. The items within a table row must be separated by at least one Tab character, but you can add extra Tabs or more spaces if you like; they’ll just be ignored.

When copying blocks of source code from one place to anotehr, such as to or from an email reader or a forum post being displayed in a Web browser, you need to be aware that some programs of this sort automatically turn Tabs into rows of spaces. The text will look the same on the screen — but if Inform is expecting a Tab, it won’t understand the text anymore!

White space is preserved in double-quoted text when it is output to the screen during the game, so when you start adding conditional code within double-quoted text, you need to be careful to put spaces only where you want them. For instance, this is a text formatting mistake:

```inform7
The description is "The bowl is [if intact] a priceless treasure [otherwise] badly damaged [end if]." [Mistake!]
```

Can you see what will happen? It looks easier to read in the source code, because we’ve separated the [] blocks by putting spaces on both sides … but when the text is printed out in the game, there will be two spaces after “is” and a space before the final period. Technically, we might not call this a bug, since your game will run perfectly, but there will be extra spaces in the sentence that appears in the game.

In writing source code, you definitely need to put white space around words. Borrowing from the example in the section on “Text Insertions,” above, this will work:

```inform7
To say bowl-desc:
```

...but this obviously won’t:

```inform7
Tosaybowl-desc:
```

There’s no penalty for adding extra spaces, however. This will work, though there’s no reason to do it:

```inform7
To say bowl-desc :
```

In some situations, you can insert one extra carriage return (an old-fashioned term, but still useful — it means, “you can start a new line at the left margin”), but not two returns. If there’s an empty line, Inform won’t like it. This will work:

```inform7
To say
bowl-desc:
```

...but this won’t:

```inform7
To say

bowl-desc:
```

In many other situations, white space doesn’t matter. As far as Inform is concerned, each sentence (that is, each block of code that ends with a period) stands on its own. You don’t even need to put a space after the period. And if the sentence is followed by a blank line, you don’t need to end the sentence with a period either. So these five ways of writing a pair of sentences are exactly the same, and all of them will work:

```inform7
Painting is an action applying to nothing.Understand "paint" as painting. [No space after period]
```

or:

```inform7
Painting is an action applying to nothing. Understand "paint" as painting. [Space after period.]
```

or:

```inform7
Painting is an action applying to nothing.
Understand "paint" as painting.
```

or:

```inform7
Painting is an action applying to nothing.

Understand "paint" as painting.
```

or:

```inform7
Painting is an action applying to nothing

Understand "paint" as painting [No periods.]
```

But this won’t:

```inform7
Painting is an action applying to nothing
Understand "paint" as painting
```

If Inform doesn’t see a period and doesn’t see a blank line either, it thinks you’ve written one long continuous statement. As a result, it can’t compile the code.

Blank lines can’t be used within code blocks, however. This won’t compile:

```inform7
Instead of looking when the location is the hall of mirrors:

        if the player is invisible:

                say "It feels weird to look in the mirrors and not see your handsome features reflected back." [Errors!]
```

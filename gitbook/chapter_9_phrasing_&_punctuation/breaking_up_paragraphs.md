## Breaking Up Paragraphs

If you write a description (most likely, a room description) that runs on for several paragraphs, you can separate the paragraphs within a single double-quoted block by using two Return/Enter key presses, like this:

```inform7
The Desolate Moor is a room. "A gloomy treeless waste stretches out on all sides. A few rocky outcrops add an air of ancient menace.

Closer to hand, a crumbling castle stands."
```

When the game is played, there will be a standard paragraph break (that is, a blank line) before the sentence, “Closer to hand....”

Another way to get the same effect is with the text insertion “[paragraph break]”:

```inform7
The Desolate Moor is a room. "A gloomy treeless waste stretches out on all sides. A few rocky outcrops add an air of ancient menace.[paragraph break]Closer to hand, a crumbling castle stands."
```

This is a better, safer way to break up multiple paragraphs when the text appears in tables and conversation responses. Note that there is no space after “break]”. We want the next paragraph to begin at the left margin. A space character in quoted text will always be printed.

Speaking of the left margin, some authors would prefer to use book-style text, in which paragraphs are indented rather than being separated by vertical blank space. Most interactive fiction doesn’t use this style. If you want to do it (I don’t recommend it), here’s how:

```inform7
The Desolate Moor is a room. "[tab]A gloomy treeless waste stretches out on all sides. A few rocky outcrops add an air of ancient menace.[line break][tab]Closer to hand, a crumbling castle stands."

To say tab:
        say " ".
```

Occasionally you may need to write two separate “say” statements and have them printed together, without a paragraph break. In this case, the tool of choice is to end the first with “[run paragraph on]”. Here’s a handy little utility that illustrates the use of “[run paragraph on]”: If the player picks up something without having examined it, the description is automatically tacked onto the output after the word “Taken.”

```inform7
A thing can be examined or unexamined.
After taking something unexamined:
        say "Taken. [run paragraph on]";
        try examining the noun.
Carry out examining something:
        now the noun is examined.
```

This code creates a new property of all things, the property “examined”, and sets the property whenever a thing is examined. But the point of the example is this: If “[run paragraph on]” isn’t included, the description of the thing that’s picked up will be on a separate line. It will look more natural if it follows immediately after the word “Taken.” is printed. Try it both ways to see the results for yourself.

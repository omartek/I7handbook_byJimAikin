## Mr. & Mrs.

In the U.S., we always put a period after abbreviations like Mr., Mrs., Ms., and Dr. In Britain no periods are used. But even if Graham Nelson weren’t British, the period has some uses in Inform that would make it tricky to handle those abbreviations.

In source text, Inform understands the period as being the end of a sentence. So you can’t create a character this way:

```inform7
Mrs. Smith is a woman in the drawing room. [Error!]
```

Inform will think “Mrs” is a separate sentence — a sentence that makes no sense. The solution is to leave out the period when creating Mrs. Smith:

```inform7
Mrs Smith is a woman in the Drawing Room. "Mrs. Smith is a stout woman of mature years." Understand "stout" and "woman" as Mrs Smith.
```

You can refer to her as “Mrs. Smith” in the description, or in any other output text that you write, but as far as Inform is concerned, she’s Mrs Smith. To fix this, we need a special rule:

```inform7
Rule for printing the name of Mrs Smith: say "Mrs. Smith".
```

One problem remains: If the player types X MRS. SMITH, the parser won’t know what the player means. Inform won’t allow periods to be used in Understand text, so we can’t do this:

```inform7
Understand "stout", "woman", and "Mrs." as Mrs Smith. [Error!]
```

Also, if the player types a command that includes a period, the parser will understand it as two separate commands. For example, the player can move quickly from room to room (assuming she knows the route) like this:

```
>n. e. n. nw
```

As far as the parser is concerned, those are four separate commands. This is a handy feature found in most modern IF interpreters. In the example above, X MRS. SMITH would produce the description of an object whose name includes the word “Mrs”, because the parser would understand the first command as X MRS — but SMITH would look to the parser like a separate command, one that is not likely to be understood. To prevent this, we have to use an advanced feature of Inform — the “after reading a command” activity. As soon as the player hits the Return/Enter key to issue a command, we’re going to look for an input that matches “MRS.” and replace it with “MRS” before the parser gets a chance to process it. While we’re at it, we’ll fix the other common abbreviations too:

```inform7
After reading a command:
        let T be text;
        let T be the player's command;
        replace the regular expression "mrs\." in T with "mrs";
        replace the regular expression "mr\." in T with "mr";
        replace the regular expression "ms\." in T with "ms";
        replace the regular expression "dr\." in T with "dr";
        change the text of the player's command to T.
```

I’m not going to try to explain every line in that code, because regular expressions are an advanced topic, not something we’ll explore in detail in the _Handbook_. If you’re curious, you can learn more by reading **Chapter 20** of _Writing with Inform_, “Advanced Text.” If you don’t have the patience for that, just copy the code above exactly, and it will do the job. (If you’re retyping it, don’t skip the backslash characters before the periods, or skip the hard-to-see periods themselves.)

The extension called Punctuation Removal by Emily Short provides a simple way of getting rid of the periods in the player’s input. This extension, which is bundled with Inform, allows us to skip typing the messy code above, and simply write:

```inform7
Include Punctuation Removal by Emily Short.

After reading a command:
        resolve punctuated titles.
```

Punctuation Removal can do several other useful tricks. You’ll find it in the Extensions tab in the IDE.

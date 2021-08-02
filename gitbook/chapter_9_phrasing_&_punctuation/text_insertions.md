## Text Insertions {#text-insertions}

It’s extremely common for the game to need to make some decisions about what to print while the game is being played. The ways to do this are well described in **Chapter 5** of _Writing with Inform_, “Text,” but we’ll look at a couple of examples here.

In our first example, a ceramic bowl can be broken or unbroken. If it’s broken, the description should obviously change. You can use square brackets to embed if/otherwise tests in the description of the bowl, like this:

```inform7
The ceramic bowl is on the end table. The ceramic bowl can be broken or unbroken. The description is "The delicate ceramic bowl is [if broken]chipped and cracked[otherwise]a beautiful work of art[end if]." Understand "delicate" as the ceramic bowl. Understand "chipped" and "cracked" as the ceramic bowl when the bowl is broken.
```

I’ve also created an Understand sentence that adds “chipped” and “cracked” as vocabulary — but only when the bowl is broken. The main point of this example, though, is the insertion of “[if broken]”, “[otherwise]”, and “[end if]” in the description. (And by the way, Inform accepts “else” as a synonym for “otherwise.” Less typing.) Notice that the period that ends the sentence is _after_ the [end if]. The period will always print out, no matter whether the bowl is broken or unbroken. This is the way I prefer to write if/otherwise/end if blocks in my games, but you can also do it this way:

```inform7
The description is "The delicate ceramic bowl is [if broken]chipped and cracked.[otherwise]a beautiful work of art.[end if]".
```

Here, I’ve moved the period inside the if/otherwise text. So I also have to add a separate period _after_ the close-quote, to let Inform know that the description sentence is finished. The advantage of doing it the first way is that the period just before the close-quote does double duty: Inform both prints it (because it’s part of the output text) and understands it as ending the sentence that begins “The description is”.

When a period, question mark, or exclamation point falls at the very end of a text block, just before the closing quotation mark, Inform understands that the punctuation mark both ends the sentence within quotes _and_ ends the larger context of the surrounding code. For example, here’s an error:

```inform7
Instead of ringing the bell:
        say "The bell produces only a dull thud."
        now the butler is suspicious. [Error!]
```

This code won’t compile. The problem is that the line beginning with “say” ends with a period. As a result, Inform thinks the Instead rule is finished — so the third line doesn’t seem (to the compiler) to belong to a rule at all. It’s just floating in code-space, not attached to anything. If we need to continue with more lines of code after a close-quote like this, we need to tack on a semicolon to tell the compiler that we’re not done yet:

```inform7
Instead of ringing the bell:
        say "The bell produces only a dull thud.";
        now the butler is suspicious. [Now the code will compile, because we added a semicolon.]
```

A tidy way to deal with this is to put the other parts of the rule _before_ the quoted output text. If you get in the habit of doing this, you won’t need to worry about adding extra punctuation. Here’s how the revised rule would look:

```inform7
Instead of ringing the bell:
        now the butler is suspicious;
        say "The bell produces only a dull thud."
```

But we were talking about text insertions, not about periods. You can string together several tests within a single block of output text by using “[otherwise if ...]”, like this:

```inform7
The ceramic bowl can be intact, chipped, or shattered. The description is "The delicate ceramic bowl is [if intact]a beautiful work of art[otherwise if chipped]slightly damaged[otherwise]shattered into shards[end if]."
```

You’ll notice that we don’t have to tell Inform _what_ object we’re asking “if intact” about. Inform knows that, by default, the object being examined is the one whose properties are being tested. We could test something entirely different, though, if we wanted to:

```inform7
The description is "[if the curator is in the location]The bowl looks quite valuable, but you don’t dare get close enough to give it a good inspection, not while the curator is hovering nearby, looking nervous[otherwise]The bowl is a Ming Dynasty vase, clearly worth millions[end if]."
```

What we can’t do is embed one if-test inside another. This type of thing won’t work:

```inform7
The description is "[if intact][if the curator is in the location]You don't want to appear too interested in the bowl while the curator is hovering about[end if]The bowl appears to be a priceless Ming Dynasty vase[otherwise if the bowl is chipped][if the curator is in the location] ...". [Error!]
```

When you need to test several conditions at once while assembling an output text, the most convenient and reliable way to do it is to use a To Say statement. We might write a To Say statement for our ceramic bowl like this:

```inform7
The ceramic bowl is on the end table. The ceramic bowl can be intact, chipped, or shattered. The description is "[bowl-desc]."

To say bowl-desc:
      	if the bowl is intact:
            		if the curator is in the location:
                  			say "You don't want to appear too interested in the bowl while the curator is hovering about";
            		otherwise:
                  			say "The bowl appears to be a priceless Ming Dynasty vase";
      	otherwise if the bowl is chipped:
            		say "The bowl is slightly chipped";
            		if the curator is in the location:
                  			say ", as you know only too well, having chipped it yourself. The curator is guarding it jealously";
      	otherwise:
            		say "The bowl is shattered beyond repair".
```

Notice the slightly unusual way those “say” lines are formatted. None of them ends with a period inside the close-quote. This is because the period that ends the description is up above, in the description property for the ceramic bowl. When you use a To Say rule in this way, you need to be especially careful about where the period is that ends the last sentence. This is because Inform does some special output formatting when it hits the end of a quoted sentence or paragraph. If the period is in the wrong place, a blank line can disappear from the output, or an extra blank line can be added.

>**Extra &amp; Missing Blank Lines in Output**
>
>A frequent problem for beginning Inform authors is that the game output has either too many blank lines in it, or not enough of them. The biggest cause of this is periods not being placed correctly at the ends of double-quoted text blocks. When you start inserting if-tests and alternate blocks into your text, this problem is more likely to show up. To avoid this situation, think logically, scrutinize your code, and test it under all of the conditions that can arise.

Three instructions are available to help you fiddle with the line breaks if you need to. You can use [line break], [paragraph break], or [run paragraph on]. All of these are worth knowing about. They’re discussed on **p. 5.8** of _Writing with Inform._

You can put any word you want in double-quoted text using brackets, as shown above, and then write a To Say statement that will run when the bracketed word is reached. Hyphenated compound words, such as “bowl-desc”, are a good choice, because they’re unlikely to be used anywhere else in your code.

Normally a To Say statement should always be called from within text that’s going to be printed out in the game. This type of thing is legal, but usually not a good idea:

```inform7
After attacking the ceramic bowl:
        say "[another-code-block]".

To say another-code-block:
        if the ceramic bowl is shattered:
                [more code goes here...]
```

Instead of using “say”, a better way to call a separate code block, if you need to do it, is just to create it using a To statement, like this:

```inform7
After attacking the ceramic bowl:
        sound the alarm.

To sound the alarm:
        if the ceramic bowl is shattered:
                [more code goes here...]
```

But there’s no requirement that the To Say rule actually print any text to the game’s output. Once in a while you may want to cause something to happen as part of a text output. Here’s a simple example — we’re going to adjust this NPC’s mood when you ask him to give you an object:

```inform7
Alexander Button can be friendly, neutral, or hostile. Alexander Button is neutral.

Instead of asking Alexander Button for the will:
        say "[Alexander-less-friendly]Alexander laughs at you."

To say Alexander-less-friendly:
        if Alexander is friendly:
                now Alexander is neutral;
        otherwise if Alexander is neutral:
                now Alexander is hostile.
```

In this example, the text output “Alexander laughs at you” includes a call to a To Say rule that prints nothing. It has only one effect: it causes Alexander to become less friendly by adjusting one of his properties. In this case, you could get the same result using a To phrase, as shown earlier in this section, by adding a line like “crank up Alexander’s hostility” in the Instead rule — but there are times (such as when printing text that’s stored in a table) when using a To Say statement is really the best way to do it.

### Switchable Markup {#switchable-markup}

As explained on **page 5.9** of _Writing with Inform_, you can switch bold and italic type on and off within the quoted text in a “say” statement. You might want to do this, for instance, to draw the player’s attention to items in a room description if the item can be examined or otherwise manipulated. This effect can be helpful to new players, but it can annoy experienced players. So we’d like to let the player switch it on or off.

The extension called Keyword Interface by Aaron Reed does this kind of thing, and a lot more besides. Here’s a simple way to do it without Keyword Interface, which may be all you need:

```inform7
Using-bold is a truth state that varies. Using-bold is false.

When play begins:
        say "Tip for new players: If you would like the game to highlight interesting objects in the room with [bold type]boldface type[roman type], use the 'bold on' command. To stop using the effect, type 'bold off'."

To say b:
        if using-bold is true:
            		say "[bold type][run paragraph on]".

To say \b:
        say "[roman type][run paragraph on]".

Bolding is an action out of world applying to nothing. Understand "bold" and "bold on" and "boldface" and "boldface on" as bolding.

Carry out bolding:
      	now using-bold is true;
      	say "Bold type to highlight interesting objects switched on."

Unbolding is an action out of world applying to nothing. Understand "bold off" and "boldface off" and "no bold" and "no boldface" and "not bold" as unbolding.

Carry out unbolding:
      	now using-bold is false;
      	say "Bold type highlighting switched off."

The Patio is a room. "In the pavement is set a small iron [b]grate[\b]."
```

The key to understanding this code is in the blocks that begin “To say b:” and “To say \b:” These test whether the truth state using-bold is true or false. Once we’ve set things up properly, we can use the text insertions “[b]” and “[\b]” to mark any item that we want highlighted with boldface type — and the player will be able to control the effect using a simple utility command.

### Quotes Within Quotes {#quotes-within-quotes}

When you start writing NPC conversations, it’s easy to forget that the quotation marks surrounding your text won’t be printed out. This, for instance, is an error:

```inform7
Instead of asking Alexander Button for the will:
        say "I would never give it to you!"
```

Here’s the output:

```
>ask alexander for will
I would never give it to you!
```

This reads like a response from the parser (that is, from the game itself), not from Alexander. The correct way to do it is using single quotes within the double quotes, like this:

```inform7
Instead of asking Alexander Button for the will:
        say "'I would never give it to you!'"
```

This produces a better output:

```
>ask alexander for will
"I would never give it to you!"
```

Now the player can see that it’s Alexander talking. A better writing style would be to include a _dialog tag_ in the text:

```inform7
Instead of asking Alexander Button for the will:
        say "'I would never give it to you!' he replies with a sneer."
```

As explained on **p. 2.3** of _Writing with Inform_, “Punctuation,” Inform will automatically turn single quotes into double quotes when formatting its output. But this raises a potential problem — how to handle apostrophes. If an apostrophe is in the middle of a word, Inform will understand that it’s an apostrophe, and won’t turn it into a double quote when outputting the text:

```inform7
Instead of asking Alexander Button for the will:
        say "'I'd never give it to you!' he replies with a sneer."
```

Here, the word “I’d” will be printed correctly. But if the apostrophe is at the end of a word, as in some types of dialect and informal speech, Inform will get confused:

```inform7
Instead of asking Alexander Button for the will:
        say "'I'm not givin' it to you!' he replies with a sneer." [Error!]
```

This code will put a quotation mark after the word givin. To get an apostrophe into the output at the end of the word givin’, we have to put brackets around it:

```inform7
Instead of asking Alexander Button for the will:
        say "'I'm not givin['] it to you!' he replies with a sneer."
```

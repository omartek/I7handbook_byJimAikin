## Actions with Topics {#actions-with-topics}

Inform provides an action called consulting it about. By default, this does nothing except print out a message that says, “You discover nothing of interest in [the noun].” The results, if the player tries LOOK UP EXPLOSIVES IN MRS SMITH, are rather comical, because Inform seems to be implying that there is actually a way of looking things up in Mrs. Smith. We’ll want to fix that. Nonetheless, we can use this action to create an encyclopedia — or for that matter, a computer terminal — in which the player can look up whatever topics we like. Here’s an encyclopedia:

```inform7
The encyclopedia is in the Library. The description is "A massive 27-volume set of the Encyclopedia Frobozzica. You could probably look up almost anything in it!" Understand "volume" and "book" as the encyclopedia.

Instead of consulting the encyclopedia about something:
say "Flipping through the encyclopedia, you learn that [run paragraph on]";
if the topic understood is a topic listed in the Table of Encyclopedia Entries:
say "[article entry][paragraph break]";
otherwise:
say "there's nothing in the encyclopedia on that topic."

Table of Encyclopedia Entries
topicarticle
"Monty Python" or "Python" or "Monty Python's Flying Circus" or "Flying Circus""Monty Python's Flying Circus was a very strange British comedy show popular in the 1970s."
"crayons" or "crayolas" or "crayon""crayons are made of wax. They come in bright colors, and are used to create works of art on paper."
"weapons" or "weaponry" or "swords" or "sword""a sword was the weapon preferred by knights in the Middle Ages. Swords are often used for hacking, slashing, and stabbing."

Instead of consulting someone about something:
        say "Does [the noun] look like an encyclopedia?"

Instead of consulting something about something:
        say "[The noun] [are] not a likely-looking source of information."
```

The main part of this code uses a _table_. Tables are Inform’s way of keeping large amounts of data organized; for more on tables, see [here](../chapter_10_advanced_topics/tables.md#tables). The main thing you need to know about tables, at the moment, is that they contain rows and columns, and that the items in each row are separated by Tab characters. There is a single return character at the end of each row.

**_Note:_** Tab characters are _not_ kept by a copy-paste action if you select the code above in Adobe Reader (Windows) or Preview (Mac) and copy it into Inform. If you do that, you’ll need to replace the Tabs yourself, in order to get the game to compile. In addition, extra return characters may be _added_ when you copy and paste text from the _Handbook._ These returns will have to be stripped out after you copy the example into Inform’s IDE.

Inform’s IDE doesn’t display Tab-separated tables any better than the word processor I’m using to write this book. As a result, a table that has long entries, like the one above, can be difficult to understand or debug just by looking at it. It’s a mess. Here’s what the table above would look like if we could use a real word processor table (which we can’t do, because Inform wouldn’t understand it):

| topic | article |
| --- | --- |
| "Monty Python" or "Python" or "Monty Python's Flying Circus" or "Flying Circus" | "Monty Python's Flying Circus was a very strange British comedy show popular in the 1970s." |
| "crayons" or "crayolas" or "crayon" | "crayons are made of wax. They come in bright colors, and are used to create works of art on paper." |
| "weapons" or "weaponry" or "swords" or "sword" | "a sword was the weapon preferred by knights in the Middle Ages. Swords are often used for hacking, slashing, and stabbing." |

With the code shown above, the player can CONSULT ENCYCLOPEDIA ABOUT SWORDS or LOOK UP WEAPONRY IN ENCYCLOPEDIA. Both commands lead to the consulting it about action, and from there to the entry in the article column in the table. If you look at the entries in the topic column for the table, you’ll find that each entry has several texts separated by the word _or._ It’s important to spell out all of the variations you think your player might try to use. The last row in the table, for instance, has no entry under topic for “weapon”, because I forgot to add one. If the player tries to LOOK UP WEAPON IN ENCYCLOPEDIA, the default response (“...there’s nothing in the encyclopedia on that topic”) will be printed out. In this case, that would be a misleading response.

The last two Instead rules in this example provide better responses for when the player tries to look up a topic in something other than the encyclopedia.

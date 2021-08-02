## Reading Matter

![](../assets/graphics23.jpg)

Inform’s standard rules assume that READ means the same thing as EXAMINE. This is not a bad assumption for a simple game. In the case of a roadside sign, the description of the sign would probably include the text printed on the sign, so there’s no need to have a special reading action. But in the case of a book or even a note on a piece of paper, we may want to make reading a separate action. Here’s how to do it:

```ìnform7
A thing has some text called the reading-material. The reading-material of a thing is usually "".

The book is in the Library. The description is "A first edition of [italic type]In Praise of Folly[roman type], by Erasmus." Understand "praise", "in praise of", "folly", and "erasmus" as the book. The reading-material of the book is "A fascinating discussion of the idiocies to which the human mind is susceptible. After reading it, you feel quite humble, and even more foolish than before".

Understand the command "read" as something new.

Reading is an action applying to one thing and requiring light. Understand "read [something]" as reading.

Check reading:
        if the reading-material of the noun is "":
                say "Nothing is printed on [the noun].” instead.

Carry out reading:
        say "[reading-material of the noun]."
```

If your game also includes things like roadside signs, for which you want READ to give the same result as EXAMINE, you could change the Check rule like this:

```ìnform7
Check reading:
        if the reading-material of the noun is "":
                try examining the noun instead.
```

Another way to do it would be to leave the Check rule saying “Nothing is printed on [the noun]” and add this for any signs:

```ìnform7
Instead of reading the roadside sign:
        try examining the roadside sign.
```

My first idea, in designing this example, was to start by saying, “A thing can be legible or illegible. A thing is usually illegible.” But after thinking about it for a minute, I realized I could simplify the code. All the Check Reading rule needs to do is find out whether the reading-material of the noun is “” (that is, whether it’s empty). Anything that has text in its reading-material can now be read. Note also that the reading-material of the book ends without a period. This is because the period is at the end of the quoted bit in the Carry Out Reading rule.

Another thing we might want to do in a game is create a book (or even a computer) in which the player can look things up. The best way to do this is by creating an action that uses the topics we want the player to look up — see “Actions with Topics” in Chapter 4 ([here](../chapter_4_actions/actions_with_topics.md#actions-with-topics)).

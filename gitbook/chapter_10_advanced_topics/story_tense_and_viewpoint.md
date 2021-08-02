## Story Tense and Viewpoint

Present tense and second person viewpoint are very widely used in interactive fiction. For instance:

```
You can see a teapot and a vicious troll here.
```

“You” is second person (English makes no distinction between second person singular and second person plural), and “can see” is present tense. But what if you’d like to write a story in first person singular, past tense? Or, more exotically, third person plural, future tense? The current version of the Inform library provides fairly full support for writing a game in any combination of tense and viewpoint, as explained on **p. 14.1** of _Writing with Inform._ In fact, you can switch tense and viewpoint at any point in the story, which might be useful if one section of the story is a flashback to an earlier time, or has a different viewpoint character.

If your game is written entirely with one tense and viewpoint, the details of how the Standard Library does this magic trick may not be of much interest. You can just put something like this near the beginning of your source code, and you’re good to go:

```inform7
When play begins:
        now the story viewpoint is first person singular;
        now the story tense is past tense.
```

This will produce output in the form:

```
I could see a teapot and a vicious troll here.
```

If you need to switch from one viewpoint or tense to another during the course of the game, you’ll probably want to make use of the same kinds of text insertions that the Standard Library uses. These methods are detailed in Chapter 14 of _Writing with Inform._

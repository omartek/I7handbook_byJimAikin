## What Does Inform 6 Have to Do with Inform 7?

In this _Handbook_, I’ve deliberately avoided getting too far into the deep end of Inform programming. If you work with Inform 7 for a while, though, you’ll start to see occasional mentions of Inform 6.

In a technical sense, Inform 7 is built “on top of” Inform 6\. Inform 6 is still being used behind the scenes when your game is compiled. But this fact is normally well hidden from the I7 programmer, and there’s no reason why most authors need to concern themselves with it.

Once in a while, an expert programmer will want to achieve an effect that can only be achieved by including some I6 code in an I7 game. If you look at the code in a few extensions written by experts, you’ll probably see Inform 6 peeking through the curtain. Here’s a line from an extension by Emily Short that I chose at random:

Use direct event handling translates as (- Constant DIRECT_GLK_EVENT_HANDLING; -).

The parentheses and hyphens are what tells the compiler “Here’s some Inform 6 code.” What that particular line does … I don’t know, and it doesn’t matter. For more details on how Inform 6 code can be included in Inform 7 code, you can look at **pages 27.14** (“Using Inform 6 within Inform 7”)through **27.24** (“Inform 6 adjectives”) of _Writing with Inform_. But the things you can do with I6 code are far beyond the scope of this _Handbook_.

Think of it this way: Writing a game in Inform 7 is like driving a car down the road. Adding I6 code to an I7 game is like pulling over, popping the hood, and tinkering with the fuel pump. Once in a while, that may be the only way to get where you want to go, but you shouldn’t need to do it too often, and nobody but an expert mechanic should try it at all.

## Things vs. Kinds {#things-vs-kinds}

New Inform writers sometimes get into trouble by using the word “kind” when it’s not needed. This word has a special meaning in Inform. It refers to types of objects — what traditional computer programmers call “classes.” The usual reason to create kinds is so that you can write code that will apply to several different objects, like this:

```inform7
A fruit is a kind of thing. The banana is a fruit. The orange is a fruit. The plum is a fruit. The apple is a fruit.

Before eating a fruit:
        say "You’re not hungry right now." instead.
```

The Before rule shown above will apply when the player types EAT ORANGE, or EAT PLUM, or EAT BANANA, or EAT APPLE. But if you should later happen to create a peach and forget to tell Inform that the peach is a fruit, the Before rule won’t be applied to EAT PEACH.

Here’s an example, adapted from a post on the newsgroup rec.arts.int-fiction, of how you can get in trouble using the word “kind” when you don’t need to:

```inform7
A phaser is a kind of thing.
A phaser can be either set to stun or set to kill.
Instead of examining the phaser, say "Your shiny Mark Five phaser. Dual setting - stun and kill. [if the phaser is set to kill]It is currently set to kill.[Otherwise]It is currently set to stun."
A phaser is usually set to stun.

The player is carrying a phaser. Understand "Mark", "Five", and "shiny" as the phaser.

[Error: will not compile!]
Instead of setting the phaser to "kill":
        now the phaser is set to kill;
        say "You set your phaser to kill."
```

The problem is that the Instead rule is attempting to change the setting not of any individual phaser but of the entire _kind._ Inform won’t let the author do that. There are a couple of ways to solve the problem. We can rewrite the Instead rule so that Inform knows which phaser to set:

```inform7
Instead of setting a phaser (called P) to "kill":
        now P is set to kill;
        say "You set your phaser to kill."
```

Here’s another way to do exactly the same thing without using the “called” phrase to create a temporary name for the object:

```inform7
Instead of setting a phaser to "kill":
now the noun is set to kill;
say "You set your phaser to kill."
```

> **Noun &amp; Second Noun**
>
>Notice the term “the noun” in the code above. The words “noun” and “second noun” have a special meaning in Inform. The noun is a temporary value (a variable) that refers to whatever object the player mentioned in the most recent command.
>
>For instance, if the player types EAT THE PIE,” the pie object becomes (temporarily) “the noun.” Likewise, the second noun is the second object in a two-object command, such as STAB TROLL WITH SWORD. Here, the troll is the noun and the sword is the second noun. You should always use “noun” and “second noun” in code (though without quotation marks, of course) when you’re not sure what object the player will be referring to. For more on variables, [here](../chapter_9_phrasing_&_punctuation/values.md#values).

Both Instead rules for the phaser will work. Either way, Inform now understands that it’s supposed to set one particular phaser to kill, and it’s happy to do so. In general, though, creating a kind and then an object that has the same name as the kind is best avoided. Sometimes it’s necessary; for instance, the door kind is built into Inform, and it would be silly to try to avoid calling a door a door. But if you can come up with a specific word for your new kinds, a word that is not used by any of the objects, you’ll create fewer confusing bugs.

Unless you’re planning to have several phasers in your game, there’s no reason to make phaser a kind in the first place. Instead, make it a plain old thing. The first sentence in the code below does exactly that:

```inform7
The player carries a phaser. The phaser can be set to kill or set to stun. The phaser is set to stun. The description is "Your shiny Mark Five phaser. Dual setting - stun and kill. [if the phaser is set to kill]It is currently set to kill.[Otherwise]It is currently set to stun." Understand "Mark", "Five", and "shiny" as the phaser.

Instead of setting the phaser to "kill":
        now the phaser is set to kill;
        say "You set your phaser to kill."
```

Now the Instead rule for setting the phaser works the way the original author of this code intended.

One reason for the confusion here, by the way, is that Inform quite often ignores “a” and “the” when compiling. There are a few situations where it notices “a” or “the”, such as when constructing lists, but in this particular case it pays no attention whatever to the difference that native English speakers would see between “a phaser” and “the phaser”.

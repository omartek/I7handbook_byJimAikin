## Creating an NPC

Creating a new non-player character is easy. Assuming we’ve created a room called the Billiard Room, we can then write:

```inform7
Troy is a man in the Billiard Room. The description is “Troy looks devilishly handsome in his tuxedo, but you’re not sure you trust him.” Troy is wearing a tuxedo.
```

The assertion, “Troy is wearing a tuxedo” both creates an object (the tuxedo) and lets Inform know that the tuxedo is wearable. (If you actually want the player to wear the tuxedo at some point in the story, you’ll have to write some code for getting it away from Troy. By default, characters won’t let go of things they’re wearing or carrying.)

In fact, the sentence “Troy is wearing a tuxedo” lets Inform know that Troy is a person, because only people and animals can wear things. By default, an object that you say is wearing something will be male and a person, not an animal. So we can delete the words “a man” in the code above and get exactly the same result. I suggest always saying that an NPC is a man or a woman, however, because if you should later change your mind about having the NPC wear something and delete the sentence about the tuxedo, the NPC will no longer be a man, just a thing.

If you use this code in a game, you’ll find that when the player enters the billiard room, the game reports, “You can see Troy here.” As you’ll recall from Chapter 3, we can improve the output by giving the Troy object an initial appearance_._ The initial appearance is formatted exactly like a room description — it appears immediately after we create Troy, and is written as a double-quoted sentence that stands by itself. The sentence below that begins, “Troy is leaning nonchalantly” is an initial appearance.

```inform7
Troy is a man in the Billiard Room. “Troy is leaning nonchalantly against a corner of the billiard table, pretending not to notice you.” The description is “Troy looks devilishly handsome in his tuxedo, but you’re not sure you trust him.” Troy is wearing a tuxedo.
```

Now, when the player enters the billiard room, the room description will include, instead of the boring line “You can see Troy here,” the much more colorful line, “Troy is leaning nonchalantly against a corner of the billiard table, pretending not to notice you.” I’d recommend always giving an NPC an initial appearance.

At present, Troy doesn’t do much. But even at this stage, Inform understands that a person is different from most other types of objects. Here’s a transcript of what can happen in the billiard room with no more code for Troy than what we’ve written above:

```
>kiss troy
Troy might not like that.

>kiss tuxedo
You can only do that to something animate.

>take troy
I don't suppose Troy would care for that.

>take tuxedo
That seems to belong to Troy.
```

As you can see, Inform automatically understands that kissing is something that the player character can do to people (or to animals), but not to inanimate objects. If we try to take a person, the default error message prevents it — and if we try to take something that a person is wearing or carrying, we get a different error message.

Incidentally, if you need the player to be able to kiss an inanimate object — perhaps you’ve created the Pope as a character, and the player is expected to kiss the Pope’s ring — you’ll find that a simple Instead rule won’t do the job. A Before rule won’t work either. This is because the Inform library defines the kissing action more or less like this:

```inform7
Understand “kiss [someone]” as kissing.
```

The grammar token “[someone]” won’t match an inanimate object; it will only match a person. So an Instead or Before rule will never have a chance to get into the act: the command KISS RING will be rejected by the game’s parser. The same thing happens, by the way, with the GIVE TO and SHOW TO actions, though those are less likely to cause problems, because it’s hard to think of a reason why you would want the player to be able to show or give something to an inanimate object!

We’ll borrow a bit from Chapter 4 of the _Handbook_, “Actions,” and show how to make it possible to kiss something inanimate. We don’t need to define a separate kissing action for inanimate things — all we need to do is add a grammar line and define a default “you can’t do that” message:

```inform7
Understand "kiss [something]" as kissing.
Instead of kissing something which is not a person:
        say "[The noun] [don't] look very sanitary."
```

Now we can write an instead rule that will allow the player to pay osculatory obeisance to Troy’s tuxedo:

```inform7
Instead of kissing the tuxedo:
say "Troy graciously allows you to kiss his tuxedo."
```

The distinction between “[someone]” and “[something]” is worth mentioning because it allows us to write new actions that will also apply only to people. For instance, we might want the player to be able to flatter other characters. Causing the flattery to affect the character would take a bit more code, but we can create a basic flattering action like this:

```inform7
Flattering is an action applying to one thing. Understand "flatter [someone]" and "praise [someone]" as flattering.

Check flattering:
        say "[The noun] blushes modestly."

Instead of flattering Troy:
        say "Troy grins at you. 'Well, sure. Anything nice you say about me, I gotta believe you mean it.'"
```

Now the player can flatter any character in the game, thereby producing the response in the Check rule above. But flattering Troy will produce a different response, and the parser won’t let the player flatter inanimate objects. Care is required when writing default responses, however, because an animal will match the grammar token “[someone]”. If you’ve got a talking tortoise in your game, you don’t want the tortoise blushing modestly when flattered!

>**“Man” & “Woman”**
>
>If you create an NPC by saying, for instance, “Troy is a man,” the parser won’t understand the word “man” as referring to Troy. This is because the name of a kind is not understood as referring to specific objects of that kind unless you say it is. You have to add the vocabulary by hand:
>```inform7
>Troy is a man in the Billiard Room. Understand "man" as Troy.
>```
>
>If you have several male characters in your game, you can handle this for all of them at once by writing:
>```inform7
>Understand "man" as a man.
>```

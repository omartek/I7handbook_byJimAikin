## [Any Thing]

Earlier in this chapter, I explained that the first step in processing an action is to make sure the object or objects that the player is talking about are in scope — that is, that they’re visible in the room. This happens because the grammar for actions (the Understand rule) normally uses the token “[something]”. The code for the new action called paint-applying, a page or two back, gives a good example.

If we want to bypass scope checking, we can change this to the token “[any thing]”. The token “[any thing]” puts every object in the game in scope, no matter what room it’s in (or, for that matter, if it’s nowhere). Please don’t bypass scope checking for casual reasons, because it will make a mess of the realistic effects that Inform tries to create. Once in a while, though, it may be useful. For instance, you could give your players more or less the same power as the debugging PURLOIN command, like this:

Acquiring is an action applying to one visible thing. Understand "acquire [any thing]" as acquiring.

```inform7
Check acquiring:
        if the player encloses the noun:
                say "You already have [the noun]." instead.

Carry out acquiring:
        now the player carries the noun.

Report acquiring:
        say "You are now carrying [the noun]."
```

Note the use of “one visible thing” in the definition of the acquiring action. When writing an action that can apply to “[any thing]”, you need to do this. Oddly enough, “one visible thing” is a more _general_ term than “one thing.” In effect, “one thing” means “one thing that the player can both see and touch,” while “one visible thing” means “one thing that is visible (but we don’t care whether the player can touch it or not)”. If you fail to specify “one visible thing”, your magic grab-anything command will fail: The parser will complain that the player is unable to reach into a distant room. In other words, the desired object will fail the touchability test.

The acquiring action might make a reasonable magic spell if your player character is a powerful wizard, able to summon distant objects, but you’ll want to be careful how you write the Check rule for it. Several things can go wrong if you let the player use this type of spell indiscriminately. As mentioned in Chapter 5, “Characters” (see [here](../chapter_5_creating_characters/conversations,_part_ii_asktellgiveshow.md#topics-of-conversation)), the “[any thing]” token is also useful for creating topics of conversation — abstract objects that are never anywhere in the model world. But if you’re doing this, and _also_ using “[any thing]” to magically manipulate objects that do appear in the model world, you need to make sure the Check rule handles all of the possibilities. If you’ve created a SHAZAM spell that can acquire distant objects and “India” exists not as a real physical object in the model world but simply as an object that can be talked about, you don’t want the naughty player to be able to do this:

```
> shazam india
With a swirl of sparkling light, India appears in your hands!
```

What’s worse, SHAZAM ME will produce a run-time error.

For an example that might be more useful, let’s suppose we want the player to be able to dig a hole. We’ll give the player a shovel, and we’ll assume the setting is outdoors. (If you have both indoor and outdoor rooms, you’ll need to do some extra checking before you let the player dig a hole!) The problem we have to solve is that the hole isn’t in scope until after the action takes place. There isn’t any hole in the room until the player digs it, so how can we arrange matters so that the player can use the command DIG HOLE?

The way to solve this little problem is to use “[any thing]”. We’ll create the hole offstage and then move it into the room when the player gives the command. Here’s a simple game that shows how to do this:

```inform7
The Forest Path is a room. "Tall trees surround you."

The player carries a shovel.

The hole is an open container. The hole is fixed in place. [The hole starts out nowhere.]

Rule for writing a paragraph about the hole:
        say "You've dug a hole here."

Digging is an action applying to one visible thing. Understand "dig [any thing]" as digging.

Check digging:
        if the noun is not the hole:
                say "[The noun] can't be excavated." instead;
        otherwise if the holder of the hole is a room:
                say "You've already dug a hole." instead;
        otherwise if the player does not carry the shovel:
                say "You scrabble around with your hands, but the dirt is pretty hard. You need a shovel." instead.

Carry out digging:
        try digging the hole with the shovel instead.

Digging it with is an action applying to one visible thing and one thing. Understand "dig [any thing] with [something]" as digging it with.

Check digging it with:
        if the noun is not the hole:
                say "[The noun] can't be excavated." instead;
        if the second noun is not the shovel:
                say "[The second noun] can't be used for excavating." instead;
        otherwise if the holder of the hole is a room:
                say "You've already dug a hole." instead;
        otherwise if the player does not carry the shovel:
                say "You can't do that unless you're actually holding the shovel." instead.

Carry out digging it with:
        move the hole to the location.

Report digging it with:
        say "You pitch in with the shovel and dig a nice deep hole."
```

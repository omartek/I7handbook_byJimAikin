## Three Types of Actions

We can separate actions into three main categories, depending on how many nouns (objects) the action applies to. Some actions take no nouns, some take one noun, and some take two. Another type of action take **topics** (that is, simple text) instead of a noun. (See “Actions with Topics” on [here](../chapter_4_actions/actions_with_topics.md#action-with-topics))

Commands like SLEEP and WAIT stand by themselves. It would make no sense at all to say SLEEP THE APPLE. Sleeping _on_ or _in_ something, such as a bed, would make sense, but the command SLEEP IN BED would trigger a different action (not the sleeping action but the sleeping in action), and you’d have to create that action yourself, because Inform doesn’t include it by default.

As this little digression should show, the same verb (in this case, “sleep”) can trigger two or even three different actions, depending on how the player’s input is phrased, and in particular depending on how many nouns are used in the command.

Commands like PICK UP THE APPLE and BOUNCE THE BALL take one noun. Commands like PUT APPLE IN BASKET and HIT BALL WITH STICK take two nouns. Two nouns are the upper limit; there’s no easy way in Inform to create a command that uses three nouns. Nor is there much reason to want to do so. The best advice I’ve read on this subject is, “If you think you actually need to create an action that requires three nouns … think about it some more.”

A possible edge case arises in the handling of objects that can’t be touched. For instance, you might want your game to allow a command such as PUT RED-HOT METAL IN WATER BUCKET USING TONGS. But such a situation can be adequately handled by implementing PICK UP METAL WITH TONGS followed by PUT METAL IN BUCKET, using suitable new rules to make sure that the action of inserting the red-hot metal object in the water bucket can only happen if the metal is already in the tongs.

While processing the player’s command, Inform refers to the first noun in the input simply as the noun. The second noun is referred to as — you guessed it — the second noun. In writing our own code, we can test the values of noun and second noun if we need to, like this:

```inform7
Instead of inserting the apple into something:
        if the second noun is the basket:
                say "The basket scoots away from you!";
        otherwise:
                continue the action.
```

In this case, we might be better off writing an Instead rule that simply refers to “inserting the apple into the basket”. But you’ll sometimes find it useful to write tests such as, “if the second noun is the basket”.

The second and third categories above use objects — what Inform calls _things_. But you can’t refer to “the thing” or “the second thing” in processing an action. The word “noun” is the tool for the job.

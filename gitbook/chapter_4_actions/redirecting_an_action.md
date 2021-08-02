## Redirecting an Action

Situations can arise in which a game needs to respond to a particular command by turning it into a different command. The tool for this is, as you might guess, the Instead rule. When the player tries one command, an Instead rule intercepts it and turns it into a different command.

Here’s a simple example. (For a slightly more complex example, see “Mr Potato Head” in Appendix C, [here](../appendix_c_short_sample_games/mr_potato_head.md#mr-potato-head)) The player is in a room called At the Foot of a Tree. Perched in the Tree is a separate room above it. The tree itself is scenery in the first room, and we want the player to be able to climb the tree. The command CLIMB TREE will result in the same action as the command GO UP:

```inform7
At the Foot of a Tree is a room. "You're standing at the foot of a tall tree. Sturdy low-hanging branches suggest that it may be easy to climb."

The tall tree is scenery in At the Foot of a Tree. Understand "sturdy" and "branches" as the tall tree.

Perched in the Tree is up from At the Foot of a Tree. "The view from up here is spectacular (though admittedly rather leafy)."

Instead of climbing the tall tree:
        try going up.
```

It may seem that we could just as easily have said, “Instead of climbing the tall tree: now the player is in Perched in the Tree.” And indeed, in the example above, that would produce pretty much the same result (although there would be a missing empty line in the output between the player’s command and the room name). But redirecting the CLIMB TREE action to the GO UP action allows us to handle more complex game situations in a graceful way.

Let’s suppose, for instance, that the player may be carrying something so heavy that it would make climbing the tree difficult or impossible. If we’ve redirected CLIMB TREE to GO UP, we only need to test this condition once. If CLIMB TREE and GO UP remain separate actions that send the player to the same destination, then we’ll have to test what the player is carrying in two different pieces of code, which makes the code harder to write and harder to debug.

Because the Instead rule shown above redirects the climbing action to the going up action, turning the tree-climbing action into a puzzle (absurdly easy, but a puzzle for all that) requires very little effort. After the code above, we add the following:

```inform7
The player carries a heavy iron anvil. The description is "The iron anvil must weigh at least a hundred pounds."

Instead of going up in At the Foot of a Tree:
        if the player encloses the anvil:
                say "You'll never be able to climb the tree while carrying something so heavy.";
        otherwise:
                continue the action.
```

Now the player will see the same “You’ll never be able to climb” message, whether he typed CLIMB TREE or UP.

Inform allows you to test what action the player is attempting, but the syntax is a little tricky. For an example that shows how to do it, see “Restraints” in Appendix C [here](../appendix_c_short_sample_games/restraints.md#restraints).

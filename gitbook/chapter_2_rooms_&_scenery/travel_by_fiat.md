## Travel by Fiat

Normally, the player moves from room to room under his own steam, by typing GO NORTH (or simply N) and so on. Once in a while, you may want to create a puzzle in which the player will be magically whisked from one room to another by taking some other action. This is easy to do. For example:

```inform7
Instead of rubbing the magic lamp:
        say "You are engulfed in a cloud of sweet-smelling pink smoke! When you emerge, coughing, you find that your surroundings have changed.";
        now the player is in the Harem.
```

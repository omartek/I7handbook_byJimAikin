## Clearing the Screen

Some authors like to clear the screen when a new section of the story begins. This can be a nice effect if the player is teleported to an entirely new time or place, for instance. Here’s how to get that effect:

```inform7
Include Basic Screen Effects by Emily Short.

Instead of pushing the big red button:
        clear the screen;
        say "[line break]";
        say "You feel a brief tingling sensation....";
        move the player to Phobos;
        if the player does not wear the helmet:
                say "A little too late, you realize you've forgotten to don your helmet. There's no air on the surface of Phobos....";
                end the story saying "You have died.";
        else:
        stop the action.
```

The key command here is obviously, “clear the screen”; the rest is just window dressing. This command is defined in Basic Screen Effects.

The reason for putting in a line break after clearing the screen is because some IF interpreters print the first line after a clear-the-screen command behind the status bar (at the top of the window), which will make it invisible. The line break will cause “You feel a brief tingling sensation....” to appear reliably on all interpreters after the screen has been cleared. Note, however, that if your game creates a status bar with two lines of text, you’ll need to use two line breaks.

## Writing on Things {#writing-on-things}

A few years back, when I was teaching an IF programming class to some younger students, One of them asked how to create a notepad that the player could write things on. A real software notepad, in which you could select words and sentences with the mouse, would be almost impossible to create in an Inform game. But creating an in-game object, such as a piece of paper or an old-fashioned slate, that the player can write on is not terribly difficult.

An object like this might even be part of a puzzle: You could use it to let the player leave a message for another character. After writing this section of the _Handbook,_ I expanded its ideas into an extension called Notepad, which you can download from the Public Library **[???]** in your Inform IDE. The extension includes an example showing how to let a character respond to written commands. The example below is more basic than the extension; it simply creates a slate that the player can write on or erase. First we’ll create a new kind of thing called a notepad. Then we’ll change the command READ (which normally triggers the examining action) and add two new actions — writing it on and erasing.

```inform7
A notepad is a kind of thing. A notepad has a text called memo. The memo of a notepad is usually "".

Understand the command "read" as something new.

Reading is an action applying to one thing and requiring light. Understand "read [something]" as reading.

Check reading:
        if the noun is not a notepad:
                say "Nothing is written on [the noun]." instead;
        otherwise if the memo of the noun is "":
                say "At the moment, [the noun] is blank." instead.

Carry out reading:
        if the memo of the noun is not "":
                say "On [the noun] you find the words '[memo of the noun].'";
        otherwise:
                say "Nothing is written on [the noun]."

Writing it on is an action applying to one topic and one thing and requiring light. Understand "write [text] on [something]" as writing it on.

Check writing it on:
        if the second noun is not a notepad:
                say "You can't write anything on [the second noun]!" instead.

Check writing it on when the second noun is the slate:
        if the player does not carry the chalk:
                say "You'd need some chalk to do that." instead.

Carry out writing it on:
        let T be text;
        let T be the topic understood;
        now the memo of the second noun is T;
        say "Writing '[T]' on [the second noun]."

Erasing is an action applying to one thing and requiring light. Understand "erase [something]" as erasing.

Check erasing:
        if the noun is not a notepad:
                say "There's nothing on [the noun] to erase." instead;
        otherwise if the memo of the noun is "":
                say "At the moment, nothing is written on [the noun]."

Carry out erasing:
        now the memo of the noun is "";
        say "You erase what was written on [the noun]."

The Lab is a room. A piece of chalk is in the Lab.

The player carries a fish. The description of the fish is "Scaly."

The player carries a slate. The slate is a notepad. The description of the slate is "Black."

Test me with "read fish / read slate / write E=mc2 on fish / write E=mc2 on slate / take chalk / write E=mc2 on slate / read slate / erase fish / erase slate / read slate".
```

Most of this example could be copied straight across into your own game. One detail that’s specific to the example is checking whether the player is carrying the chalk before letting her write on the slate. If your game uses a piece of paper as the notepad object, simply change the piece of chalk to a pencil.

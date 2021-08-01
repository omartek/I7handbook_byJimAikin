## Punctuation {#punctuation}

Inform is fussy about punctuation, but you have some options. In conditional tests that have only one line, you can use a comma and then go right on in the same line rather than hitting a colon, a return, and adding another Tab indent. These two examples both work, and they do the same thing:

```inform7
Instead of taking the ceramic bowl:
        if the bowl is shattered, say "What would be the point?";
        otherwise continue the action.

Instead of taking the ceramic bowl:
        if the bowl is shattered:
                say "What would be the point?";
        otherwise:
                continue the action.
```

Inform also lets us skip the indentation entirely and substitute the word “begin” followed by a semicolon:

```inform7
Instead of taking the ceramic bowl:
if the bowl is shattered begin;
say "What would be the point?";
otherwise;
continue the action;
end if.
```

This example is organized using Inform’s semicolon syntax, which allows indents using Tabs, but doesn’t require them. (For more on this syntax, see the section on “Indenting,” later in this chapter.) Note that if we’re using the semicolon syntax, there is _no_ comma after “if the bowl is shattered”, and we have to back out of any “if” test by saying “end if” when we’re done with it. In code that makes several if-tests, a block formatted this way may end with several “end if” statements in a row.

If we’re using the semicolon syntax, as shown immediately above, Inform not only doesn’t care about indents, it doesn’t care whether we include carriage returns at all. We could just as easily write it this way (though it’s much harder for humans to read):

```inform7
Instead of taking the ceramic bowl: if the bowl is shattered begin; say "What would be the point?"; otherwise; continue the action; end if.
```

Of the four examples above, I prefer always to use the format in the second one. When I use a consistent format, it’s easier for me to spot mistakes.

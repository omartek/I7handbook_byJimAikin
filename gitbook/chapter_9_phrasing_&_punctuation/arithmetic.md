## Arithmetic

Traditionally, computer programming languages are well supplied with slick features for doing advanced mathematical calculations. Such calculations are very seldom needed in interactive fiction. Nonetheless, Inform has a surprising amount of power in this area, including the ability to use real numbers in scientific notation, to derive square roots, to utilize trigonometric functions such as sine and tangent, and so on. These features are explained in Chapter 15 of _Writing with Inform._

Most stories will only need to keep track of a few simple integers, for the purpose of counting things. The tool for this is the number variable.

When we need to create and use a number variable (also known as “a number that varies”), we can do it globally, or we can attach it to an object as a property of that object. It’s pretty much up to you to choose which form you prefer. The first way (making it a global value) leads to easier typing, but programmers who have some experience in object-oriented languages sometimes prefer, as a matter of style, to attach data to objects. If you have several objects (such as a room full of clocks) that use similar number variables, attaching the variables to the objects as properties would definitely be the way to go. Here’s how to create a number using each of those methods:

```inform7
[Global:] Parrot-squawk-count is a number that varies. Parrot-squawk-count is 0.

[Object property:] The parrot has a number called squawk-count. The squawk-count of the parrot is 0.
```

In effect, the second sentence initializes the variable to a value. The value can later be changed by your code.The syntax for making the change depends on how you’ve defined the variable to begin with:

```inform7
increase parrot-squawk-count by 1; [if it’s a global value]

increase the squawk-count of the parrot by 1; [if the number is a property of the object]
```

(A note for experienced programmers: All of the properties of an Inform object are public. That is, they’re available to any other code in the game. It’s not possible to make a property private: Inform does not support data hiding. So the distinction between global variables and properties is purely one of personal style. There is no functional difference.)

We can test the current value of a variable like this:

```inform7
if the squawk-count of the parrot is greater than 7:
        now the parrot is dead.
```

The syntax for these operations is outlined on **p. 15.5** of _Writing with Inform_, “Arithmetic.” Other tests that we can use include:

```inform7
if the squawk-count of the parrot is 7;
if the squawk-count of the parrot is at least 7;
if the squawk-count of the parrot is less than 7;
if the squawk-count of the parrot is at most 7;
```

Rather than write out words like “is at least,” we can for the most part use the familiar mathematical symbols. However, Inform doesn’t allow the use of = or == (the double equals sign) to test for equality. Testing for equality must use “is”. The latter three of the four tests above could be written as:

```inform7
if the squawk-count of the parrot **Illegal HTML tag removed :**
if the squawk-count of the parrot &lt; 7;
if the squawk-count of the parrot &lt;= 7;&lt; p&gt;
```

**Warning:** If you’re compiling to .z5, .z6, or .z8, the largest numbers Inform can handle are a little over 30,000 (which should be plenty for counting parrot-squawks). If you need to use larger numbers, you’ll have to compile your game to Glulx.

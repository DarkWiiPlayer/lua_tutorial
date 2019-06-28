<!-- vim: set noexpandtab tabstop=4 :miv -->

Lua, from the bottom up
================================================================================

This tutorial is intended for people with no background in programming whatsoever.
It aims to teach the basic features of Lua and all necessary programming concepts.
It is *not* a general tutorial for programming beyond this scope.

<!-- TODO: Installation -->
<!-- TODO: Notations -->

A first example
--------------------------------------------------------------------------------

Let us start with something simple: Cooking.

A simple recipe for pancakes requires you to mix the following:

	4 eggs
	400 ml of milk
	200 g of flour

	Just mix them together, heat a pan, pour in just enough pancake mix until it
	covers the entire surface of the pan and wait until it doesn't stick to the pan.
	Turn it around and wait a few more minutes. Done!

As it turns out, that's quite a lot though.
Let's say we want to use just 1/4 of those quantities.

Luckily for us,
Lua can do additions, subtractions, multiplications, etc. out of the box.
It also has a concept of "numbers".
This is common among modern programming languages,
but shouldn't be taken for granted.

In an interactive Lua shell,
we can simply type the following:

	> 4 / 4
	1.0
	> 400 / 4
	100.0
	> 200 / 4
	50.0

Good. We've conquered our first problem using Lua.
So far we've only used it as a glorified calculator though.
Let's take things further and see what else Lua can do for us.

Thinking about pancakes got me quite hungry.
Let's make twice as many pancakes, just to make sure.

At this point you might have noticed that this means we have to type in the
exact same thing again, but with a `2` instead of a `4`.

This is where things start to get interesting.
Let's generalize the problem a bit:
The recipe doesn't really change,
so those numbers are always the same,
but how much of it we want to actually use can really be anything.
Some day we may want to go with 3/4 of what the recipe says, or even 4/5.

Luckily, there's a convenient mechanism that allows us to reuse code,
and run the same program several times with different parameters:

Functions
--------------------------------------------------------------------------------

A simple function definition could look like this:

	> function flour(factor) return 200 * factor end

And we can then execute (aka. call) the function by typing

	> flour(0.5)
	100.0

Let's have a closer look at the first piece of code.
What's going on there?

### Function Definition

The `function` keyword is part of the Lua language. It tells Lua that what
follows is going to be a function definition.

The name `flour` is the name we give to the function. We can choose whatever we
want here, with some reasonable limitations (More on those later)

The braces `(` and `)` delimit the functions *arguments*, aka. its parameters,
both when it is defined and when it is called.

`factor` is another name we can choose for ourselves; it's the name by which we
can later reference the parameter that the function takes.

`return` means that what follows is the "result" of the functions execution.

The `end` keyword tells Lua that the function definition ends here.

### Function Call

Once we've defined the function,
in other words, told Lua what the function should do,
we can use it.

To do so, we simply type the name we previously gave the function,
followed by all the necessary arguments in braces.
In this case, we only needed one argument: `factor`.

Defining one function for every ingredient we need doesn't help us much though.
Sure, writing `flour(0.5)` instead of `200 / 2` means we don't have to remember
the original quantity, but we still have to write 3 lines. Let's improve that!

Instead of writing three separate functions,
let's combine them into one that calculates the three quantities we need:

	> function pancakes(factor)
	>> return 4*factor, 400*factor, 200*factor
	>> end
	> pancakes(0.5)
	2.0     200.0   100.0

Note how, when we write `function pancake(factor)` and press *enter*,
Lua is smart enough to see that this line doesn't work on its own,
so it just asks for more input (the lines starting with `>>`) until it sees the `end`,
at which point it knows what to do with the 3 lines of code.

The fact that you can `return` many values separated by commas is somewhat of a
special feature of Lua. Most other languages will only allow you to return a
single value from functions.

Okay, so far so good.
But you may have noticed that it's hard to tell what quantity relates to which
ingredient. Let's fix that now.

So far we haven't really considered *output*. The Lua interpreter was nice
enough to write the result of each line of code to the screen for us,
but what if we want to make our output a bit fancier?

`print` to the rescue!

	> function pancakes(factor)
	>> print(4 * factor)
	>> print(400 * factor)
	>> print(200 * factor)
	>> end
	> pancakes(0.5)
	2.0
	200.0
	100.0

`print` is a function that's already defined by default in Lua. It takes one or
more arguments and writes them out, separated by *tab* characters and at the end
it puts a newline character, so every time we call `print`, the output appears
on a new line.

# Let-syntax for Proton

Introducton
===========

This proposal will introduce `let` expressions in two forms:

1. As a way of introducing values into a local context
2. As a way of declaring an immutable reference to some value

1\) is referred to as the _expanded_ `let` expression or `let-in` expression,
and 2) is referred to as simply `let` expression or `let` declaration.

For both the expanded `let` expression and the `let` declaration there is
the possibility of allowing multiple declarations in the `let` block.
I believe we should possibly start out with just allowing one declaration,
as the later addition of multiple declarations is rather trivial.
(On the paper and in the grammar, at least.)

Proposal
========

Local Context
-------------

Usually one would declare and use a value as such:

    double pi = 3.14;
    double pi2 = pi * 2;

After the declaration of `pi2` the value of `pi` lingers on and clutters
the namespace when declaring a new variable.
A `let` expression would be used to introduce scoping to a value declaration.
The above example would be rewritten such that the variable `pi` only
exist when declaring `pi2`.
Using the suggested syntax for `let` expressions, the above example
would be written as such:

    double pi2 = let pi = 3.14 in pi * 2;

Now, the variable `pi` exists only for the expression `pi * 2`.

Grammar
=======

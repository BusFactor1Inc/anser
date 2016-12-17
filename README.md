anser - a boolean propagator network framework
----------------------------------------------

'Anser' is a small framework for the creation of boolean logic
computation networks from C++ expressions.  Such networks are
collections of 'wires' (terminals) that connect 'ops' (gates) to
specify boolean functions.

The created networks are non-directional; all computations *will* be
computed and output to the relvant terminal of the computation network
given sufficient information on the remaining termnals.

Information can be entered 'bit by bit' into the terminals, and the
computation graph can then be analyzed for changes in the network.  By
analyzing the changes in the nodes in the graph, it was thought that
one could use this 'emergent' information in the system to glean find
interesting information within the function that is being analyzed.

This libary could also be used to do digital logic design at the
And/Or/Not gate level.

Example
-------

```c
#include "anser.h"

int main(int argc, char** argv) {
    // Declare the I/O terminals for our network
    Bus a, b, c;

    // Define/build the computation network
    c = a + b;

    // Evaluate the network by setting terminal values.
    // Compute b, by setting a and c.
    c.set(3);
    a.set(1);

    // Make sure we're correct.
    assert(b.get() == 2);
}
```

Examples
--------

The following contain more complex examples of the system:

tests.cpp	: basic tests for computational networks.

sha256.cpp	: a (mostly) unmodified sha256 implemementation and test;
 		  changes were made to variable types to allow for the use of anser.

Graph Traversal
---------------

Wires offer the functions 'size' and 'nth', allowing for one to
retrieve the connetion Ops of the wire.

UnOps have get_in() and get_out() to retrieve thier terminal Wires.

BinOps have get_in1(), get_in2() and get_out() to retrieve thier
terminal Wires.

Ops have more than 1 or 2 input/output terminals and follow the above
convention.

Classes
-------

Wire		- a communication channel for connecting inputs and output termninal on a *Op

Bus	   	- a bundle of 'Wires', 32 by default to be used as integer expression variables
                  utilizing the overloaded integer operations to build the computation networks

--

UnOp		- 1 terminal operation

BinOp 		- 2 terminal operation

Op 		- n terminal operation

--

Id : UnOp	- input passes through to output

Not : UnOp 	- output = !input

And : BinOp	- output = input1 & input2

Or: BinOp	- output = input1 | input2

Xor: BinOp	- output = input1 ^ input2

HalfAdder: Op	- half adder with a, b, outputs sum and carry

FullAdder: Op   - full adder with a, b, carry, outputs sum and carry

--
Burton Samograd
burton.samograd@gmail.com
2016
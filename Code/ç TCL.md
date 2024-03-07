# TCL


TO START:

open terminal, type: tclsh

TO INITIATE A SCRIPT (WITH TK FUNCTIONALITY FOR GRAPHICS), TYPE: wish [name of function]

Or just type 'wish' if you want to enable TK functionality at the command line.

SOME COMMANDS:

puts: outputs a string

set: assigns a value to a string

unset: clears the variable

expr: evaluate a mathematical expression; is followed by braces containing the expression.

OPERATORS

eq: compare two strings for equality

ne: compare two strings for inequality

SYNTAX

* strings (with multiple words/elements) within braces and/or quotes are evaluated together as a single argument.

* to index the value of a variable, call it with the '$' in front of it. This will produce the value of the variable rather than its name.

* a backslash at the end of text will cause the interpreter to ignore a newline, meaning you can continue a single argument or line of code on the next line without interrupting the line.

* grouping strings within braces { } disables substitution. The only exception is the backslash at the end of text within braces, which is still used as a line continuation character.

* square brackets are for summing together different arguments for a single output (as opposed to appending strings together, as with braces and quotes)

* For math operations, use braces after the command expr.
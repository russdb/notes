[[vue]][[vue basics]][[directives]] [[vue v-bind]]
Some directives, such as v-bind, take arguments. The v-bind directive is used to bind a value to an HTML attribute.

![[vue v-bind simple.png]]

v-bind is the name of the directive, and type is the argument: in the name of the attribute we want to bind the given variable to. buttonType is the value

works with properties, such as disabled and checked:

![[vue v-bind with property.png]]

v-bind with a lot of attributes, it can be pretty repetitive to write it out multiple times. There’s a shorter way to write it: you can omit the v-bind part of the directive and use a colon.

Whether you choose to use v-bind or the shorter syntax, try to keep it consistent. Using
Inheritance is one object gets access to the properties and methods of another object.

# Classical Inheritance
Is very verbose. Is fragile.

# Prototypal Inheritance
Flexible, extensible.

All objects have access to the `proto` property. If we try to access a property that doesn't exists in an object, JS will try to find it in its `proto` property, if if doesn't find it, it will try in the proto's `proto` property, this is called the Prototype Chain.

Thanks to this Prototype Chain we can use methods like `push, filter, etc` with every JS array we create, all the arrays inherit from the base Array Object, they all have a reference to that Prototype.
# Syntax Parsers

They're intermediate programs that read code and determine what it does and it its grammar is valid.

# Lexical Environment

Where something sits physically in the code you write.

# Execution Context

A  wrapper to help manage the code that is running. It contains the code you wrote, but it can also contain additional code. Like the execution created by the browser that contains the "this" variable. [[10. The Global env and the Global Object]].

It contains the Global Object, "this" and a reference to its Outer Environment [[17. Scope Chain#Outer Environment]].

# Execution Stack

Is a stack that keeps track of all the Execution Contexts.

# Name/Value Pair

A Name which maps to a unique value.

# Object

A collection of name/value pairs.

# Undefined

Undefined is a special value, that means that a variable hasn't been set. This value is set during the Creation Phase of the Execution Context.

# Single Threaded

One command executed at the time.

# Synchronous Execution

One command at a time, in order.

# Function Invocation

Calling a function. By using a parenthesis.

# Variable Environment

Where the variables live, and how they relate to each other in memory. Each Execution Context has its own Variable Environment.

# Event Queue

It is a data structure that holds events that are waiting to be executed. It works in conjunction with the Event Loop.  
  
It allows the browser to handle events asynchronously.

The events are only processed after the Execution Context is Empty, this means that Long Running functions can block the execution of JS.

# Primitive Type

A type of a data that represents a single value.
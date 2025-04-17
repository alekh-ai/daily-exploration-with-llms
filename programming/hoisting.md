# Hoisting

While JavaScript is the most prominent language associated with the term "hoisting," some other languages exhibit behaviors that share similarities, particularly concerning the ability to refer to functions before their explicit definition in the code. However, the underlying mechanisms and the extent to which variables are also affected differ.

Here's a breakdown of languages with hoisting-like behavior:

**1. Python:**

- **Functions:** Python allows you to call a function that is defined later in the same file. This works because Python compiles the entire file into bytecode before execution. During this compilation phase, the interpreter becomes aware of all function definitions.
- **Variables:** Python **does not** hoist variable declarations. You must assign a value to a variable before using it; otherwise, you'll get a `NameError`.

**2. PHP:**

- **Functions:** Similar to Python, PHP allows calling functions before their definition. This is due to the way PHP parses and executes scripts.
- **Variables:** PHP **does not** hoist variable declarations in the same way as JavaScript's `var`. If you use an uninitialized variable, PHP will issue a notice, and the variable will have a default value (usually `null` or an empty string, depending on context). However, it's not the same as `undefined` in JavaScript, and it's generally considered bad practice to rely on this.

**3. Compiled Languages (C, C++, Java, etc.):**

- These languages are generally **not considered to have hoisting** in the same sense as interpreted scripting languages. They are statically typed and compiled ahead of time.
- **Functions:** They often use **forward declarations** (also known as prototypes in C/C++) to inform the compiler about the existence and signature of a function that will be defined later or in a different compilation unit. This allows calling the function before its full definition appears in the current code. However, this is a mechanism for the compiler to understand the interface, not a runtime behavior of moving declarations.
- **Variables:** In compiled languages, you generally need to declare a variable before using it. Using a variable before its declaration will typically result in a compile-time error. C and C++ have the concept of **forward declarations** for variables using the `extern` keyword, but this signifies that the variable is defined elsewhere, not that the declaration is moved. Java does not generally allow forward referencing of instance variables in a way that their use precedes their declaration within the class if it leads to uninitialized use.

**Key Differences from JavaScript Hoisting:**

- **Variables:** The most significant difference is in how variables are treated. JavaScript's `var` hoisting, with the `undefined` initialization, is quite unique. Other languages generally either require declaration before use or handle uninitialized variables differently.
- **Mechanism:** In interpreted languages like Python and PHP, the ability to call functions before definition arises from the compilation/parsing phase making the interpreter aware of the functions early on, not from a literal movement of code. Compiled languages use forward declarations as a compiler directive.

**In summary, while Python and PHP allow calling functions before their definition, a behavior somewhat similar to JavaScript's function hoisting, they do not exhibit the same variable hoisting behavior. Compiled languages use forward declarations for functions as a compiler aid, which is distinct from the runtime behavior of hoisting in JavaScript.**

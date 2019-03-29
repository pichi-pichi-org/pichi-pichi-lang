- Feature Name: `variables`
- Start Date: 2019-03-29

# Summary
[summary]: #summary

Variables are a necessity to a good templating language. Being able to assign data to a variable promotes easier re-usability of that variable and all around better user experience. This rfc encompasses what a variable is, what a valid variable name is, and how can one declare a variable and assign a value to it in a statement.

# Motivation
[motivation]: #motivation

Variables are an invaluable necessity for pichi-pichi. Just like in other programming languages, variables help us out by providing a way of labeling data with a descriptive name, so that the program can be understood more clearly by the reader and ourselves.

# Guide-level explanation
[guide-level-explanation]: #guide-level-explanation

- A **variable** in pichi-pichi is the same as a variable in other languages like C# or C++
- A **variable declaration** uses the `let` keyword to denote the start of a variable declaration
- A **variable name** can start with a letter or underscore `_` and followed by a letter `A-Z a-z`, a digit `0-9`, or an underscore `_`
- A **variable** can be assigned a value using a single equals sign `=`
- A variable's value can be any type of `string`, `number`, `boolean`, `object` or `array`

The structure to a valid variable starts with `let`, followed by the variable name, followed by the equals sign `=`, and then followed by the value.

Here's a valid variable declaration and assignment:

```
{{ let x = 5 }}
```

Remember that an expression is delimited by a line break or a semicolon `;`, so that if you want to assign multiple variables in one line then it can look like this:

```
{{ let x = 5; let y = 3; }}
```

Or with the last semicolon omitted:

```
{{ let x = 5; let y = 3 }}
```

Or using a line break:

```
{{ 
  let x = 5
  let y = 3
}}
```

You can also declare a variable but not assign it to anything. This will then have a value type of `undefined`.

```
{{ let x }}
```

Or, with an optional semicolon:

```
{{ let x; }}
```

You can combine this to later assign the variable a value:
```
{{ let x }}
...
...
...
{{ x = 5 }}
```

Furthermore, any variable can be reassigned a value.

```
{{ let x = 6; let y }}
{{ x = 3 }}
{{ y = 1 }}
```

If a user forgets to assign a value to variable, then an error should be thrown that could look like this:

```
input:1:11 error PPCHI0003: Unable to evaluate value on the rhs of the variable.

1 {{ let x = }}
```

# Reference-level explanation
[reference-level-explanation]: #reference-level-explanation

Valid variable names include:

- `city`
- `City`
- `cITY`
- `_city`
- `C_ity`
- `___city___`
- `C4T5`
- `c12_3`

Invalid vairable names include:

- `12city`
- `#213city`
- `@!$%^&*()_+`


Valid variable declaration and assignment include:

- `{{ let x = 4 }}`
- `{{ let city = 5 }}`
- `{{ let c=6 }}`
- `{{let x= 4}}`
- `{{ let a  =  6}}`

Invalid variable declartion and assignment include:

- `{{ let x = }}`
- `{{ let let = 5 }}`
- `{{ let 5 = hello }}`
- ```
  {{
    let x = 
    5
  }}
  ```

# Drawbacks
[drawbacks]: #drawbacks

> empty

# Rationale and alternatives
[rationale-and-alternatives]: #rationale-and-alternatives

The variable naming scheme follows those like in C++ and C#. It's a proven scheme that should fit well for pichi-pichi.

# Prior art
[prior-art]: #prior-art

> empty

# Unresolved questions
[unresolved-questions]: #unresolved-questions

> empty

# Future possibilities
[future-possibilities]: #future-possibilities

> empty

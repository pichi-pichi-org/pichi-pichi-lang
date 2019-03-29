- Feature Name: `statement_and_expression`
- Start Date: 2019-03-28

# Summary
[summary]: #summary

The statement syntax relates to the syntax used for code blocks that enclose pichi-pichi related code. Expressions are what go inside statement blocks.

# Motivation
[motivation]: #motivation

We need to have the syntax set it stone for how we should recognize when pichi-pichi code starts and when it ends. In addition, we should recognize when an expression starts and ends.

# Guide-level explanation
[guide-level-explanation]: #guide-level-explanation

A pichi-pichi statement can be thought of as a block of code that does something. Whether that's using
built-in methods or variable assignment, etc.

A statement can be grouped together as one statement using double curly brackets like so:

```
{{ expression }}
```

For experienced programmers, you can think of pichi-pichi statements as the same for other languages
like C, C++, or C# that use single brackets to define a statement.

In C++, a valid statement looks like so:

```
int main()
{
    int x = 0;
    return x;
}
```

A similar statement in pichi-pichi could look like so:

```
{{ let x = 0 }}
{{ x }}
```

If a user forgets to properly close a statement, then an error should be thrown that could look like this:

```
input:2:15 error PPCHI0001: Unable to parse closing statement bracket.

2 {{ expression }
```

Or, if they forget to type the start statement properly but type the closing tag correctly:

```
input:2:2 error PPCHI0002: Unable to parse starting statement bracket.

2 { expression }}
```

A pichi-pichi expression can be anything from a variable declaration to a control-flow expresssion. Expressions in pichi-pichi are delimited by a line a break or a semicolon `;`. Use of the semicolon allows multiple expressions to exist on the same line like so:

```
{{ expression1; expression2; expression3; }}
```

You can also omit the last semicolon right before the closing statement bracket if you feel the need to do so:

```
{{ expression1; expression2; expression3 }}
```

When using line breaks, semicolons become completely optional.
Here's an example for multiple expressions on different line breaks: 

```
{{
    expression1
    expression2
    expression3
}}
```

This is also valid:

```
{{
    expression1;
    expression2;
    expression3;
}}
```

As well as this:

```
{{
    expression1;
    expression2
    expression3
}}
```

# Reference-level explanation
[reference-level-explanation]: #reference-level-explanation

To start a pichi-pichi statement, use double left curly brackets: `{{`

To end a pichi-pichi statement, use double right curly brackets: `}}`

A valid statement has a pair of double left and double right curly brackets:

```
{{ expression }}
```

Start or end brackets that exceed a count of 3 and more are considered invalid
statements.

The following is an invalid statement: `{{{ expression }}}`

Additionally, the following statements are also invalid:

- `{ expression }`
- `{ expression }}`
- `{{ expression }`
- `{{{ expression }}`
- `{{{ expression }}}}}`
- `{ expression }}}}}`

Expressions in pichi-pichi are delimited by a line a break or a semicolon `;`. Use of the semicolon allows multiple expressions to exist on the same line. When using line breaks as delimiter, then semicolon becomes completely optional.

# Drawbacks
[drawbacks]: #drawbacks

As of right now, I don't see any drawback to the double bracket syntax. It looks cleaner then liquid's (`{% ... %}`) in my opinion and should be sufficient enough for this language. Additionally, the expression syntax follows in the footsteps like other languages such as JavaScript and I cannot see any downsides to it as far as readability and usage.

# Rationale and alternatives
[rationale-and-alternatives]: #rationale-and-alternatives

As said before, double brackets for pichi-pichi statements look cleaner. It promotes an easier readability experience. I want to follow the zen of Python that less is more, simple is better than complex,and readability counts. I feel that the cleaner and simpler the syntax, then the easier it is for people to understand what's going on. The double bracket syntax follows this idea. The expression syntax also follows this idea. 

I don't see any alternatives to the double bracket syntax. It's the best choice for the job. Similarly, the expression syntax should fit well into the pichi-pichi language.

# Prior art
[prior-art]: #prior-art

After examing other templating solutions that have followed in the path of Liquid or Handlebars I have come to the following conclusion. It seems that other solutions work fine if escape hatches are provided to escape the delimiter or change the delimiter entirely.

As you can see here:
- https://github.com/ericf/express-handlebars/issues/85
- https://github.com/wycats/handlebars.js/issues/227

It seems like mixing templating languages like Angular + Handlebars seems to be problematic.
There are workarounds like escaping the delimiter as seen in this solution:

```html
<h2>{{thisIsForHandleBars}}</h2>
<p>\{{thisIsForAngular}}</p>
```

But the slight difference between a backslash and no backslash could be frustrating for developers.
Having the ability to map the start and end delimiters to something else lies in making the lexer configurable.

# Unresolved questions
[unresolved-questions]: #unresolved-questions

- Should we make the lexer configurable to allow remapping of the start and end delimiters for pichi-pichi statements? The default could still be double curly brackets.

# Future possibilities
[future-possibilities]: #future-possibilities

Having a configurable lexer and the ability to remap the start and end delimiter for statements seems invaluable. Seeing other templating languages have this issue means we should consider addressing this issue from the start.

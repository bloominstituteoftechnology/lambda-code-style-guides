# Lambda Swift Style Guide

Code is more often read than written. It's not just the compiler who cares about your code. Your code should be clear, simple, conventional, and well documented to create the most lasting and maintainable artifact of your efforts.

Each language has its quirks and techniques and each one its own dialect. Despite that, certain universal truths underlie the crafting of code across languages and use-cases.

Good programmers write good code: code that is consistent and readable. A consistent style simplifies reading and understanding. Many companies provide "style guides", documents that describe house-style conventions. This guide explores Lambda's house-style. As a student, we expect you to learn and adopt the conventions in this guide.

Many style choices are subjective or arbitrary. Good programmers disagree about the best choices in many cases. Regardless of your personal likes and dislikes, regardless of your stance on commas or colons, each member of a team is expected to select and follow the house style to the best of their abilities and to use that style when evaluating and other people's code within the same organization.

Our style is based on conventional industry coding. 

## Correctness

Correctness is not a style. It's a prerequisite. And that's why it is the first topic covered here in this style guide. Your code must compile without warnings. Code that produces warnings by definition does not meet our code style standards. When a warning is unavoidable, you must document the reason behind that warning. Where appropriate, instruct the the compiler to ignore it, to better bring your code in line with this first rule. 

## Lambda Core Style

Here are the basic elements of style we expect you to adopt here at Lambda:

* Lambda uses 4-space indentation, not tabs, not 2-spaces.
* Lambda leaves spaces after commas, so `item1: Int, item2: Int`, not `item1: Int,item2, Int`.
* Lambda uses left-magnetic colons, so `value: Int`, not `value:Int` and not `value : Int`.
* Lambda omits spaces within parentheses: `(1, 3)`, not `( 1, 3 )`.
* Lambda always leaves spaces between braces and co-linear text, so `{ return }`, not `{return}`.
* Lambda omits parens around `if` and `switch` conditions, so `if condition` not `if (condition)`.
* Lambda uses UpperCamelCase names for types and protocols. User lowerCamelCaseNames for type members including properties and methods. Avoid underscores except as prefixes specifically meant to indicate private variable use.
* Lambda uses meaningful names. "i" is not a meaningful name, nor is "j" or "k", or "prop1" or "vc" or "uitvc". Prefer to use appropriate words that relate to roles, such as `for (key, value) in dict` and `for index in array.indices` and `for value in sequence`. 
* Lambda prefers multi-line clauses:
```
if index == count { // prefer
   continue
}

if index == count { continue } // not preferred
```
* Lambda avoids forced unwrapping, preferring guard statements with coherent fatal error messages that explain why unwrapping an optional failed:
```
let url = URL(string: "...")!
guard let url = URL(string: "...") else {
    fatalError("Unconstructable URL")
}
```
* Lambda uses the default `weak` form for `@IBOutlet`. It is acceptable to remove the `weak` keyword and use strong outlets so long as you do so consistently across your project.
* Lambda uses `Void` return types, not `()`. Prefer `-> Void` for closure arguments over `-> ()`.
* Lambda omits semicolons, and especially trailing semicolons in its code. Use "statement" not "statement;"
* Prefer `.toggle()` to `someBool = !someBool", prefer `string.isEmpty` to `string.count == 0` or `string == ""`.

## Organization

Your projects and your code should be well organized. As a project grows in complexity, you should be able to easily navigate through the code it contains. Xcode groups serve organization by breaking down projects into related items that support each other on a basic level. However, remember that grouping is meant to serve maintainability and ease of file access. It is not a barrier between the coder and a human maintainer of that code.

In general, a single `.swift` file contains one type (struct, class, or enum) or protocol. Make exceptions for closely related types, and for protocols exported by the primary type in a file.

## Comments

Code should be self-documenting whenever possible, with comments reserved for explaining **why** a particular piece of code does something.

## Naming

Descriptive and consistent naming makes code easier to read and understand. The Swift project offers an [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/#naming) document that documents the accepted naming conventions for the Swift community. You should read this document, and follow its conventions. Some key points:

- **Swift is succinct**. Include all the words needed to avoid ambiguity, but omit needless words.
- **Names are role-based**. Name variables, parameters, and associated types according to their roles, rather than their type constraints.
- **Function signatures are grammatical**. You should be able to speak function names and their arguments out loud and the result will be meaningful. Prefer method and function names that make use sites form grammatical English phrases. For example, `x.insert(y at: z)`, not `x.insert(y, position:z)`
- **Side-effects drive names**. Name functions and methods according to their side-effects. For example, `x.distance(to: y)` has no side effects, and is a noun phrase. `x.sort()` has side effects (it modifies `x`), and therefore reads as an imperative verb phrase.
- Uses of Boolean methods and properties should read as assertions about the receiver. For example, `x.isEmpty`, and `line1.intersects(line2)`
- **Name protocols with nouns and adjectives**. Protocols that describe what something _is_ should read as nouns (e.g. `Collection`). Protocols that describe a _capability_ should have the suffixes `able`, `ible`, or `ing` (e.g. `Equatable`, `ProgressReporting`).
- **Avoid obscure terms**. Don’t say “epidermis” if “skin” will serve your purpose.
- **Avoid abbreviations**. Abbreviations, especially non-standard ones, make your code significantly less clear and readable. For example, `button`, not `btn`. 
- **Prefer methods and properties over free functions.**. Free functions, that is functions declared at the global scope, should only be used in special cases. Instead, nest functions into the most natural parent type as static members.
- **Internal parameter names are important.** Even though they don't appear where a function is called, internal parameter names make function signatures, function implementations, and documentation easier to read.
- **Default argument values simplify common uses.** Any parameter with a single commonly-used value is a candidate for a default. Prefer to locate parameters with defaults toward the end of the parameter list.
- **Label tuple members and name closure parameters** where they appear in your API.
- **Avoid single letter placeholder type names.** When using generics in your code, do not use placeholder types such as `T`, `S`. etc. instead opting for descriptive names such as `Type`, `Element`, `Number`, etc.

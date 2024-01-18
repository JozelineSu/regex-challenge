# Regular Expressions

Regular expressions (regex) are patterns used to check if a string is made up of characters that match the given expression. Regex has many use cases, such as:

    - Validating user input
    - Analyzing blocks of text
    - Searching code

You build regular expressions using literal and meta characters. A literal character just means that the pattern is searching for an exact match. For example, in this line of code: 

    /abc/

The only acceptable string would be "abc", it has to be those characters in that order- no exceptions. However, meta characters allow for a more dynamic search pattern. "*" is a meta character that used if you want to allow a specific character to appear 0 or multiple times and you put it after the character. For example, "abbbbbbbc" would match the pattern set by this regex:

    /ab*c/

## Summary

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

The regex seen above is used to validate acceptable hex values. Using this expression, I will describe the meaning of each part of this expression and how it is able to check for hex values.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

Below we will discuss the components that make up a regular expression.

### Anchors

Anchors are metacharacters that are used to describe a position in a string. Both "^" and "$" are anchors. This can be seen in our hex value regex:

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

The carat signifies the start of string and the dollar sign matches the end of a string. They are the most commonly seen anchors used to ensure your string begins or ends in a certain way. 

### Quantifiers

Quantifiers indicate how many times you want a specific character or expression to appear. Our hex value regex has many examples: 

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

    - ?
    - {6}
    - {3}

The question mark indicates that the "#" is optional. If you want to specify how many times you want to match a character/expression, you use curly brackets ( {} ). "{6}" tells us that this expression 
"[a-f0-9]" needs to have six characters, same for the "{3}" quantifier. 

### OR Operator

The OR operator is the vertical bar( | ) used to separte multiple pattern choices that we want or regex to check. As it is used in our hex value regex, we are looking for either this expression 
"[a-f0-9]{6}" or "[a-f0-9]{3}".

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

### Character Classes

Character classes are used to represent a set of literals that you want to match. They are good to minimize coding and are surrounded by square brackets ( [] ). In our hex value regex we can see these character classes: 

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

    - [a-f0-9]

Instead of writing out what letters and numbers our regex accepts, [abcdef0123456789], we used a character class to simplify the code and make it more readable. There are also recognized character classes you can use as shortcuts for example:

    - \w :used as substitute for [A-Za-z0-9]
    - \d :used for [0-9]
    - \s :used for [ \t\r\n\v\f]

Furthermore, there are also ways to manipulate character classes if you wished. Such as, using the caret symbol to symbolize that you want the pattern to search for characters NOT in the character class. So, "[^0-9]" would mean that the pattern searches for anything but a number.

### Flags

Regex components are contained between the forward slashes surrounding the entire regular expression. The only exception to this rule are flags. Flags are regex components that change how the regular expression is processed. Some common ones are:

    - i :Stands for ignoreCase, makes regex case insensitive
    - g :Stands for global, allows regex to be a global search
    - m :Stands for multiline, allows ^ and $ to match newline characters

### Grouping and Capturing

Grouping is when you put a set of characters together and surround them by parantheses. When you group characters together it means you want to see them as a single unit. In our hex value regex we group together two sub-expressions separating them with an OR operator:

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

Capturing memorizes parts of the matched string so you can reuse them later. You can reuse these parts by recalling their number. Since capturing groups are automatically numbered by the orfer of their opening parantheses.

### Bracket Expressions

Brackets indicate a set of characters to match. 

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

For example in our hex value regex we have 
"[a-f0-9]", which means we want the expression to search for letters a-f followed by numbers 0-9.

### Greedy and Lazy Match

Another aspect of quantifiers is greedy or lazy matches. By default, a regular expression is greedy, meaning it will repeateadly try to match the regex as much as possible. On the other hand, lazy quantifiers will attempt to match the expression the least number of times possible. It is represented by a question mark, which will try to match the character 0 times if possible. This can be seen in our hex value regex, where we try to match the hash character ( # ) zero times:

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/
    - #?

### Boundaries

Boundaries are referred to as delimiters, which in our case are the forward slashes ( / ). They are the first element of a regex and will contain the entire expression of the attern we want to match. As shown in our hex value regex:

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

### Back-references

A back-reference refers to a previously captured group being used in the same regular expression. The syntax for a back-reference is "\n", n being the number of the captured group you want to recall.
For example, "/\b(\w+)\s\1\b/" the "\1" refers to this captured group "(\w+)" and the line of code will search through blocks of text and find word duplicates.

If we run "/\b(\w+)\s\1\b/" on this paragrapsh:

    On a sunny sunny day, the dog comes out to play. The really really young children are always happy to play with the dogs. They run run around until they get tired and the sun goes down to rest. Only when the sun sleeps do the tired tired children lay their heads.

We would get back these matches: "sunny sunny", "really really", "run run", and "tired tired".

### Look-ahead and Look-behind

A look-ahead assertion will look at the string ahead of its current position and try to match it with the given pattern. In a positive look-ahead, if it matches the pattern the position stays the same. But in a negative look-ahead the position would change. Their syntax is:

    /(?=...)/                        positive
    /(?!...)/                        negative

A look-behind assertion has the same logic as a look-ahead, but, it will try to match the string behind its current position to try to match it with the given pattern. Similarly, it can also be negative or positive. It's syntax is:

   /(?<=...)/                        positive
   /(?<!...)/                        negative

## Resources

Mdn Web Docs [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions]
Beginner's guide to regular expressions b Carl Alexander [https://carlalexander.ca/beginners-guide-regular-expressions/]

## Author

https://github.com/JozelineSu


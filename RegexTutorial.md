# Regex Tutorial (with Email)

## Overview

A Regular Expression or "REGEX" for short, is a sequence of characters that define a search pattern. These patterns are usually used by algorithms that are string-searched to "find," or "find and replace" operations in a string. It also looks for input validations. This is a technique which is very commonly used in the computer science space.

Using REGEX we can look for a string of code.

Example: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`

The regular expression below can be used to verify that user input is a valid email address:

>`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`

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

### Anchors

* `^abc$`	-^start / $end of the string
    * `^` Matches the beginning of the string, or the beginning of a line if the multiline flag (m) is enabled.This matches a position, not a character.
    * `$` Matches the end of the string, or the end of a line if the multiline flag (m) is enabled. This matches a position, not a character.

* `\b\B`	-word, not-word boundary
    * `\b` Matches a word boundary position between a word character and non-word character or position (start / end of string). See the word character class (w) for more info.
    * `\B` Matches any position that is not a word boundary. This matches a position, not a character.
    * See Boundaries for more detailed Information
   
E-mail Regex:  `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`
<br> - Email Example: `validemail@gmail.com`


Starts the check at the start of the email address and ends the check at the end of the string.

### Quantifiers

Quantifiers indicate that the preceding token must be matched a certain number of times. These can be classified as "greedy" or "lazy".

* `a*a+a?`	-0 or more, 1 or more, 0 or 1
    * "+" Matches 1 or more of the preceding token.
    * "*" Matches 0 or more of the preceding token.
    * "?" Matches 0 or 1 of the preceding token, effectively making it optional.
    * "?" Makes the preceding quantifier lazy, causing it to match as few characters as possible. By default, quantifiers are greedy, and will match as many characters as possible.

* `a{5}a{2,}`	 -Looks for exactly five, two, or more
* `{2,6}`  	    -forces the input of characters between two and six characters long.
* `a+?a{2,}?`	 -matches as few as possible
* `ab|cd`	    -match ab or cd

E-mail Regex:  `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`
<br> - Email Example: `validemail@gmail.com`

 `+` first follows the character set: `[a-z0-9_/.-]`.
 This checks for 1 or more of those allowed characters: `(validEmail)`.
 `{2,6}` follows the character set: `[a-z\.]`.
 This quantifier says "Match between 2 and 6 of the preceding characters: `(.com)`.

### OR Operator

* `|` Acts like a boolean and/or matches the expression before or after the |.
It can operate within a group, or on a whole expression. The patterns will be tested in order. Just as in java will match either set of characters. It will look for this OR that.

### Character Classes

Character classes match a character from a specific set. There are a number of predefined character classes and you can also define your own sets.

* `[ABC]` Characters inside brakets will match any character in the set.
* `[^ABC]` Adding a caret will match any character that is not in the set.
* `[A-Z]` Add a dash between two characters will select a Range.
* `.` Will Match any characters expect linebreaks. Its like a wildcard and will accpet any input.
* `[\s\S]` A character set that can be used to match any character, including line breaks, without the dotall flag. An alternative is [^] carrot in brackets, but it is not supported in all browsers.
* `\w` Matches any word character (alphanumeric & underscore). Only matches low-ascii characters (no accented or non-roman characters).
* `\W` Matches any character that is not a word character (alphanumeric & underscore).
* `\d` Matches any digit character (0-9)
* `\p` Matches a character in the specified unicode category.

E-mail Regex:  `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`
All characters that are  contained in the email address example are allowed by the Character Classes a-z, 0-9, /d, /., and @ these still are considered  valid

### Flags

Expression flags change how the expression is interpreted. Flags follow the closing forward slash of the expression.

* `i` Ignores case
* `g` Global search retain the index of the last match, allowing subsequent searches to start from the end of the previous match. Without the global flag, subsequent searches will return the same match.
* `m` Multiline flag When the multiline flag is enabled, beginning and end anchors (^ and $) will match the start and end of a line, instead of the start and end of the whole string.
* `u` Unicode
* `y` The expression will only match from its lastIndex position and ignores the global (g) flag if set. Because each search in RegExr is discrete, this flag has no further impact on the displayed results.
* `s` Dot (.) will match any character, including newline.

E-mail Regex:  `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`
<br> - Email Example: `validemail@gmail.com`

There is one global occurrence of this email address.


### Grouping and Capturing
* `(ABC)` Capturing groups multiple tokens together and creates a capture group for extracting a substring or using a backreference.
* `(?<name>ABC)` named capturing group captures groups of a specific name.
* `\1` is a numeric Referance
* `(?:ABC)` Groups multiple tokens together without creating a capture group.

E-mail Regex:  `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`
<br> - Email Example: `validemail@gmail.com`
* Group 1 is `validemail`
* Group 2 is `gmail`
* Group 3 is `.com`

### Bracket Expressions

A bracket expression enclosed in square brackets is a regular expression that matches a single character, or collating element. If the initial character is a circumflex ^, then this bracket expression is complemented.

See Character Class to see some examples.

E-mail Regex:  `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`
<br> - Email Example: `validemail@gmail.com`

All characters in `validemail@gmail.com` fulfill the bracket expressions constraints.

### Greedy and Lazy Match

* 'Greedy' means matching the longest possible string.
    A Greedy quantifier lets the engine know to match as many instances of its quantified token as possible. This is referred to as greedy.

* 'Lazy' means matching the shortest possible string.
    A lazy quantifier lets the engine know to match as few of the quantified tokens needed. In the table below, a regular quantifier is made lazy by attaching a ? question mark to it.

See [link]"https://javascript.info/regexp-greedy-and-lazy for more detailed information.

E-mail Regex:  `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`
- Greedy Quantifier Used: `+` , `{2,6}`
    >* no lazy quantifiers were used

<br> - Email Example: `validemail@gmail.com`


### Boundaries

The `\b` is an anchor like the caret and the dollar sign. It matches at a position that is called a “word boundary”. This match is zero-length.

Characters that are matched by the short-hand character class `\w` are the characters that are treated as word characters by word boundaries.

Since digits are considered to be word characters, `\b4\b` can be used to match a 4 that is not part of a larger number. So saying `\b` matches before and after an alphanumeric sequence is more exact than saying “before and after a word”.

`\B` is the negated version of `\b`. `\B` matches at every position where `\b` does not. Effectively, `\B` matches at any position between two word characters as well as at any position between two non-word characters.

There are more boundaries with the Regex Engine. Some examples include GNU, TCL, as well as POSIX.

### Back-references

Back-references are used to match the same text that was previously matched by a capturing group. Suppose you want to match a pair of opening and closing HTML tags, and the text in between. By putting the opening tag into a backreference, we can reuse the name of the tag for the closing tag.

For Example: `<([A-Z][0-9]*)\b[^>]*>.*?</\1>` This regex contains only one pair of parentheses, which capture the string matched by `[A-Z][0-9]*`. This is the opening HTML tag. The backreference `\1` references the first capturing group. `\1` matches the exact same text that was matched by the first capturing group. The `/` before it is a literal character. It is simply the forward slash in the closing HTML tag that we are trying to match.

### Look-ahead and Look-behind

* `(?=ABC)` is a postive lookahead and it matches a group after the main expression without including it in the result.
* `(?!ABC)` is a negitive lookahead and it specifies a group that can not match after the main expression (if it matches, the result is discarded)

* `(?<=ABC>)` is a postive lookbehind and matches a group before the main expression without including it in the result.
* `(?<!ABC)` is a negitive lookbehind and Specifies a group that can not match before the main expression (if it matches, the result is discarded).

Lookaheads and lookbehinds forces the main expressions to be what you have defined it as. Without it being exactly what it is it will not be accepted as a valid input.

## Author

Jonathan Gordon - UCF Coding Bootcamp

### Sources and References
    [regexr] (https://regexr.com/)

    [BackRef] (https://www.regular-expressions.info/backref.html)
    
    [RegExpression](https://www.regular-expressions.info/wordboundaries.html)
    [RegExpression](https://www.regular-expressions.info/email.html)

My Github [github] https://github.com/JGordon59

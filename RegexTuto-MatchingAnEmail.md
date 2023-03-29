# Matching an Email: /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

The term Regex stands for Regular Expressions which are a sequence of patterns used to match character combinations in strings. In character form, it's defined as: (.*) The . means any character and the * means matches the pattern 0 or more times (commonly referred to as a wild card).

## Summary

I will be discussing the Regex code for matching an email: /^([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6})$/ This series of characters are a search pattern meant for any email validation. Consequently, it applies the rules of a valid email and if any email doesn't follow this pattern it wil be considered invalid. As a starter, below is a simple break-down of what I will discuss in detail, in terms of the characters:

() divides in sections the structure of a valid email

a-z means the string can contain any lowercase letter between a–z

0-9 means the string can contain any number between 0–9

. within the () provides the possibility of a period exisiting, while outside the () indicates that there must be a period at that point

_ - the string can contain an underscore or hyphen respectively

adds the sections together to make it one

@ means there must be an @ symbol at this given point

\d means any number between 0-9

{2,6} The string (in this case the last section: ([a-z.]{2,6}) is between 2–6 characters long
## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [Character Escapes](#character-escapes)

## Regex Components

A regex is considered a literal, so the pattern consisting of meta-characters(possible characters) must be wrapped in slash characters (/). If we examine the “Matching an Email” regex, you'll see that this is true:

/^([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6})$/

The slashes are seen at the beginning and end to state that this code equals a literal with the possibility of the meta-characters within the slashes to create a valid email.

The following are the explained components of this Regex:

### Anchors

The characters ^ and $ are both considered to be anchors.

The ^ anchor signifies a string that begins with the characters that follow it. This could be in one of two formats:

An exact string match, such as ^Apple, where the strings "Apple" or "Apple trees" match, but "apple" and "apple trees" do not. This is because a regex is case-sensitive.

The $ anchor signifies a string that ends with the characters that precede it. Just as with the ^ character, it can be preceded by an exact string or a range of possible matches.

So in our “Matching an Email” regex, the string must start and end with something that matches the pattern ([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6}). You'll notice that we didn't include the pattern {2,6}, which precedes the $ character. Why? Because this is a special component called a quantifier. We'll come back to quantifiers in a moment.

Let's take a look at the pattern ([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6}) and see what it means

### Quantifiers

Quantifiers set the limits of the string that your regex matches (or an individual section of the string in our case). They frequently include the minimum and maximum number of characters that your regex is looking for.

Quantifiers are inherently greedy, meaning they match as many occurrences of particular patterns as possible. They include the following:

*—Matches the pattern zero or more times

+—Matches the pattern one or more times

?—Matches the pattern zero or one time

{}—Curly brackets can provide three different ways to set limits for a match:

{ n }—Matches the pattern exactly n number of times

{ n, }—Matches the pattern at least n number of times

{ n, x }—Matches the pattern from a minimum of n number of times to a maximum of x number of times

Each of these quantifiers can be made lazy by adding the ? symbol after it, meaning it will match as few occurrences as possible.

In our “Matching an Email” regex, we have the quantifier {2,6} within an individual section ([a-z.]{2,6}). This means that we want to find this particular string pattern a minimum of 2 times and a maximum of 6 times. This particular string consists of the characters between a-z and a period (.).

The following examples match:

.co

com

.gov

co

The co string is a match because it meets the minimum requirement of 2 characters, and the characters are all lowercase characters. .gov is a match because it is 4 characters long (within the minimum and maximum character limits of 2 and 6) and includes a combination of lowercase characters and a period. Remember that because our regex pattern is entirely inside a bracket expression, the string doesn’t need to meet all of the requirements—just any of them.

The following examples do not match:

CO

CO2m

.Gov5erMent

.1co

The CO string is not a match because it only contains uppercase charaters. CO2m includes uppercase characters and numbers. .Gov5 has 11 characters, and the maximum limit for this regex is 6, has a number and uppercase letters. .1co includes numbers, which aren't allowed in this regex.

### Grouping Constructs

The primary way to group a section of a regex is by using parentheses (()). This is visible in our regex as it divides it up into 3 sections. The first section is ([a-z0-9_.-]+), the second section is ([\da-z.-]+) and the third section is ([a-z.]{2,6}). Let's break these sections down by utilizing an email example:

christopher750@gmail.com broken down into these three sections would be:

Section 1 ([a-z0-9_.-]+): christopher750 Section 2 ([\da-z.-]+): gmail Section 3 ([a-z.]{2,6}): .com OR com

### Bracket Expressions

Anything inside a set of square brackets ([]) represents a range of characters that we want to match. These patterns are known as bracket expressions, but they are also known as a positive character group, because they outline the characters we want to include. We can write these expressions to include all of the characters we want to match. For example, [abc] will look for a string that includes a or b or c, regardless of the length of the string. So all of the following examples would match: "apple", "trash" "cccc", "wild", "bbcd" and "endeavor".

You'll more commonly see a hyphen (-) used between alphanumeric characters (letters and numbers only) to represent a range of those possible characters. This means that [a-c] and [abc] will look for the exact same thing. In this case we have [a-z] which includes all the letters in the alphabet.

In our “Matching an Email” regex example, we can break down the bracket expressions as follows:

[a-z]—The string can contain any lowercase letter between a–z. Keep in mind that this looks for lowercase characters only. If we wanted to include uppercase characters, we would need to change the expression to [a-zA-Z].

[0-9]—The string can contain any number between 0–9

[_-]—The string can contain an underscore or hyphen. Both the underscore and the hyphen are called special characters. Special characters include any non-alphanumeric characters, such as punctuation or symbols. In this case, we only want a string that includes _ or -. It's important to note that the hyphen here is not the same hyphen that we used in our alphanumeric ranges. In bracket expressions, special characters that we want to include follow alphanumeric character ranges within the brackets.

If we put all of these expressions together so that our pattern is [a-z0-9_-], this will match any string that includes any combination of lowercase letters between a and z, any number between 0 and 9, and the special characters of an underscore or a hyphen. Keep in mind that these characters can be in any order. It's also important to note that this pattern does not require the string to meet all of these requirements; it can meet any of them.

The following examples fulfill the requirements of this regex:

"chr"

"chr750"

"ch4r_1"

"c-hr"

"1234578"

"--"

What about the string "Chr"? This would not match our pattern because it includes an uppercase character, C.

It's important to note that a bracket expression can be turned into a negative character group by adding the ^ symbol to the beginning of the expression inside the brackets. A common example is matching a string that doesn't include any vowels. The pattern [^aeiouAEIOU] would find any strings that don't include lowercase or uppercase vowels.

### Character Classes

A character class in a regex defines a set of characters or combined characters to mean a certain thing or fulfill a match.

\d—Matches any Arabic numeral digit. This class is equivalent to the bracket expression [0-9]. This is seen in our regex.

\D matches a non-digit character as it performs the inverse of \d.

### Character Escapes

Character Escapes define characters that change from literal character to meta - characters. For example, the backslash (). When a backslash is within a bracket expression, it becomes a meta - character.

([a-z0-9_.-]+) The backslash within this expression is a meta - character (can be utilized but not a must).

([\da-z.-]+).([a-z.]{2,6}) The backslash between these two sections is a literal character (must be utilized).

## Full Break Down

The Regex /^([a-z0-9_.-]+)@([\da-z.-]+).([a-z.]{2,6})$/ in terms of the email christopher750@gmail.com is:

([a-z0-9_.-]+) = christopher750 @ = @ ([\da-z.-]+) = gmail . = . ([a-z.]{2,6}) = com

Example of other matching emails:

chris@upmost.co.ke

([a-z0-9_.-]+) = chris @ = @ ([\da-z.-]+) = upmost.co . = . ([a-z.]{2,6}) = ke

Example of non-matching email:

vbXxx.com

([a-z0-9_.-]+) = Not correctly included @ = Not included ([\da-z.-]+) = Not included . = . ([a-z.]{2,6}) = com

Therefore, this email is invalid!

## Author

My name is Christopher M. Lebreton, a junior Developer from Paris, France with a passion to master the art of coding. You can find my work at: https://github.com/Beurre-moutarde

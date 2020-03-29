# Regular Expressions

## [Cheat Sheet](https://launchschool.com/books/regex/read/conclusion#cheat-sheet)

In the following tables, unescaped `a`, `b`, and `z` characters denote regular characters (letters, digits, punctuation), while unescaped `p` and `q` characters indicate patterns (each pattern may be arbitrarily complex). Other characters are literals.

### Basic Matching

| Pattern        | Meaning                                       |
| -------------- | --------------------------------------------- |
| `/a/`          | Match the character `a`                       |
| `/\?/`, `/\./` | Match a meta-character literally              |
| `/\n/`, `/\t/` | Match a control character (newline, tab, etc) |
| `/pq/`         | Concatenation (`p` followed by `q`)           |
| `/(p)/`        | Capture Group                                 |
| `/(p|q)/`      | Alternation (`p` or `q`)                      |
| `/p/i`         | Case insensitive match                        |

### Character Classes and Shortcuts

| Pattern          | Meaning                                         |
| ---------------- | ----------------------------------------------- |
| `/[ab]/`         | `a` or `b`                                      |
| `/[a-z]/`        | `a` through `z`, inclusive                      |
| `/[^ab]/`        | Not (`a` or `b`)                                |
| `/[^a-z]/`       | Not (`a` through `z`)                           |
| `/./`            | Any character except newline                    |
| `/\s/`, `/[\s]/` | Whitespace character (space, tab, newline, etc) |
| `/\S/`, `/[\S]/` | Not a whitespace character                      |
| `/\d/`, `/[\d]/` | Decimal digit (`0-9`)                           |
| `/\D/`, `/[\D]/` | Not a decimal digit                             |
| `/\w/`, `/[\w]/` | Word character (`0-9`, `a-z`, `A-Z`, `_`)       |
| `/\W/`, `/[\W]/` | Not a word character                            |

### Anchors

| Pattern | Meaning                                   |
| ------- | ----------------------------------------- |
| `/^p/`  | Pattern at start of line                  |
| `/p$/`  | Pattern at end of line                    |
| `/\Ap/` | Pattern at start of string                |
| `/p\z/` | Pattern at end of string (after newline)  |
| `/p\Z/` | Pattern at end of string (before newline) |
| `/\bp/` | Pattern begins at word boundary           |
| `/p\b/` | Pattern ends at word boundary             |
| `/\Bp/` | Pattern begins at non-word boundary       |
| `/p\B/` | Pattern ends at non-word boundary         |

### Quantifiers

| Pattern     | Meaning                                |
| ----------- | -------------------------------------- |
| `/p*/`      | 0 or more occurrences of pattern       |
| `/p+/`      | 1 or more occurrences of pattern       |
| `/p?/`      | 0 or 1 occurrence of pattern           |
| `/p{m}/`    | `m` occurrences of pattern             |
| `/p{m,}/`   | `m` or more occurrences of pattern     |
| `/p{m,n}/`  | `m` through `n` occurrences of pattern |
| `/p*?/`     | 0 or more occurrences (lazy)           |
| `/p+?/`     | 1 or more occurrences (lazy)           |
| `/p??/`     | 0 or 1 occurrence (lazy)               |
| `/p{m,}?/`  | `m` or more occurrences (lazy)         |
| `/p{m,n}?/` | `m` through `n` occurrences (lazy)     |

### Common Ruby Methods for Regex

| Method            | Use                                 |
| ----------------- | ----------------------------------- |
| `String#match`    | Determine if regex matches a string |
| `string =~ regex` | Determine if regex matches a string |
| `String#split`    | Split string by regex               |
| `String#sub`      | Replace regex match one time        |
| `String#gsub`     | Replace regex match globally        |

### Common JavaScript Functions for Regex

| Method           | Use                                 |
| ---------------- | ----------------------------------- |
| `String.match`   | Determine if regex matches a string |
| `String.split`   | Split string by regex               |
| `String.replace` | Replace regex match                 |

-   **Patterns** are the building blocks of **regex**. You construct regex from patterns using **concatenation** and **alternation**. You then place the resulting pattern between two `/` characters.
-   Concatenation and alternation of two patterns create a new pattern.
-   The most basic patterns match a single character, a range of characters, or a set of characters.
-   We call some special characters **meta-characters**; they have special meaning inside a regex. When you must match one literally, **escape** it with a leading `\` character.
-   **Character class** patterns match any character in a set or range of characters or any combination of sets and ranges.
-   **Anchors** force a regex to match at a specific location inside a string.
-   A **quantifier** matches a pattern multiple times; they always apply to the pattern to the left of the quantifier. Quantifiers are **greedy** by default, but also have **lazy** forms.
-   Parentheses let you combine patterns as a series of alternates. They also provide a way to **capture** parts of a match for later reuse; when used this way, we call the groups **capture groups**. We can access captured values with **backreferences**.



## [Variants](https://launchschool.com/books/regex/read/conclusion#variants)

Regex have variants; though most have similarities to each other, the different **engines** also have noticeable differences.  For instance, Ruby supports the `\A` and `\z` anchors, while JavaScript does not.

Other languages besides Ruby and JavaScript support regex: Perl,  Python, PHP, Awk, C/C++, Java, and more all provide varying levels of  support for regex. Even editors like vim, emacs, Atom, and Sublime Text, as well as command line tools like sed and grep use regex. Nearly every language and program has a slightly different take on regex, though.

Every regex engine should support the following features:

-   basic single character matches, e.g., `/a/`.
-   concatenation, e.g., `/pq/`.
-   meta-characters escapes, e.g., `/\*/`.
-   character classes, e.g., `/[abc]/` and `/[a-m]/`.
-   `*` quantifiers, e.g., `/a*/`.
-   `.` matches any character except a newline.
-   `^` and `$` line anchors

Other regex engines may not support some of the features we discussed. For instance, `\A`, `\z` and `\Z` aren't available with most older engines. Some features may require  escapes to designate meta-characters (the convention today is that we  use escapes when we want to match literals). In Ruby and JavaScript, for example, you can use `/(p|q)/` for alternation, but in `vim`'s default mode, you must use `/\(p\|q\)/` instead.

Some programs even let you specify the engine you want to use. Typically, you have a choice between **basic** (the default), **extended**, and **POSIX** engines. You often find this choice with modern versions of ancient programs like `awk`, `sed`, and `grep`.

Most modern programs cover all or most of the features we have  discussed, perhaps with slight variations and various levels of custom  enhancements.

## [Resources](https://launchschool.com/books/regex/read/conclusion#resources)

While this book covers almost everything you need to get started with regex, it doesn't pretend to be a reference or complete. There is much  more to even the most basic implementations, so read the documentation.  Familiarize yourself with the features that your regex engine supports,  but don't try to memorize them; that sometimes encourages overuse of  regex and the construction of regex with too much complexity. When you  find that you need a feature, go ahead and look it up.

Your first place for information should be the documentation for your language's regex implementation. Since regex engines differ, sometimes  considerably, ensure you're using the right information. The  documentation is the best insurance against misunderstandings.

Despite the engine differences, most have a common subset of features and work in the same general way. Thus, most online discussions of  regex are useful regardless of which language you use. Don't avoid sites because they use the wrong engine. Here are a few sites that may be  useful:

-   [Essential Guide To Regular Expressions: Tools and Tutorials](https://www.smashingmagazine.com/2009/06/essential-guide-to-regular-expressions-tools-tutorials-and-resources/)
-   [Regular-Expressions.info](http://www.regular-expressions.info/)
-   [Regex Tutorial—From Regex 101 to Advanced Regex](http://www.rexegg.com/)

And don't forget about [Rubular](http://Rubular.com) and [Scriptular](http://Scriptular.com) as well!

Developers frequently recommend two books as good regex resources:

-   [Introducing Regular Expressions](http://shop.oreilly.com/product/0636920012337.do)
-   [Mastering Regular Expressions](http://shop.oreilly.com/product/9780596528126.do)

The former is a thorough introduction to regex and how to use them.  It even covers advanced regex features, such as look-ahead and  look-behind assertions. The latter assumes that you are familiar with  the basics of regex, and takes you out to the deep waters where you can  explore, in excruciating technical detail, nearly every facet of regex  and their implementations.

## [Where To Go From Here](https://launchschool.com/books/regex/read/conclusion#where-to-now)

Congratulations! You've made your first dive into the regex ocean,  and returned to shore, unharmed. You should have a good grasp on how to  construct regex, and how to employ them in your programs. At the same  time, you may be a little doubtful of how much you remember. Fear not.  It takes time and practice to learn how to use regex. The more you use  them, the less difficulty you will have using them, and the more  opportunities you'll find to use them. Skillful use of regex can make  for concise, easy-to-read and understand programs.

However, don't get carried away; a regex packs a lot of meaning into a small area and can be challenging to understand six months after you  write it. If you think a regex that you are writing may be too hard to  understand, you may be right. Take a step back and see if you can  simplify the problem; sometimes, for instance, it's better to write  multiple regex than to write one large one.

Don't forget to use Rubular and Scriptular; these two sites are  incredibly useful when constructing regex. By giving them appropriate  test data, you can play with and fine-tune your regex until it does what you want it to do.

Above all, keep practicing!





------

**concatenation**	the ability of regexes to string together multiple patterns to form a larger, more-complex pattern

**alternation**	a simple way to construct a regex that matches one of several sub-patterns, using a pipe (ex. -- `/(cat|dog)/`)

**meta-characters**	characters that have special meaning in regexes  ($ ^ * + ? . ( ) [ ] { } | \ /)

**control character escape**	a backslash placed before a met-character in order to interpret it as a literal, removing its special meaning

**character classes**	patterns that let you specify a set of characters that you want to match, enclosed by brackets (ex. -- [a-x] matches any of the letters from a to x, once)

​	Note: Meta-characters in character classes are fewer:

​		`^ \ - [ ]`

**flag**	a single character placed after the closing forward slash which alters default pattern-matching behavior (ex. -- `/dog/i` matches 'DOG', 'Dog', 'doG', etc.)



https://rubular.com/

/s/	matches all elements which contain an 's'

Ruby

```ruby
str = 'cast'
print "matched 's'" if str.match(/s/)
print "matched 'x'" if str.match(/x/)
# matched 's'
```

JS

```javascript
var str = 'cast';
if (str.match(/s/)) {
  console.log("matched 's'");
}

if (str.match(/x/)) {
  console.log("matched 'x'");
}
# matched 's'
```



**Meta-characters**	chars that have special meaning in a Ruby/JS regex 

​	`$ ^ * + ? . ( ) [ ] { } | \ /`

If you want to match a literal meta-character, you must *escape* it with a leading backslash (`\`). To match a question mark, for instance, use the regex `/\?/`. 

Rubular does not detect a single space as a regex. Try `/[ ]/` instead - this is equivalent to `/ /`, but it works in Rubular.



## [Alternation](https://launchschool.com/books/regex/read/basic_matching#alternation)

In this section, we introduce alternation, a simple way to construct a regex that matches one of several sub-patterns. In its most basic form, you write two or more patterns separated by pipe (`|`) characters, and then surround the entire expression in parentheses. For example, try the regex `/(cat|dog|rabbit)/` with the following strings:

```
The lazy cat.
The dog barks.
Down the rabbit hole.
The lazy cat, chased by the barking dog,
dives down the rabbit hole.
catalog
The Yellow Dog
My bearded dragon's name is Darwin
```



## Basic Matching

In this section, we'll get our feet wet in the calmer waters of the regex ocean with a quick introduction to regex patterns, namely those that match substrings. We'll also touch on some more intricate patterns, namely those that can match one of two or more subpatterns.

We will run most of our examples through [Rubular](http://Rubular.com), so please go ahead and open it now. You can enter each pattern, and see what happens when you attempt to match them against a variety of different strings. Watch for how Rubular highlights matched characters; it shows you what your regex matches. Note that you can enter multiple lines in the test strings area.

JavaScript programmers can use [Scriptular](http://Scriptular.com) instead of Rubular to test regex. However, there are some differences in behavior from Rubular. Our narrative uses Rubular's behavior; avoid confusion and use it for this book even if you're learning regex for JavaScript.

Note that Rubular provides the `/` characters that delimit regex. You shouldn't enter the `/` characters yourself when entering them in Rubular. However, remember that you need them in your programs.



## [Alphanumerics](https://launchschool.com/books/regex/read/basic_matching#alpha-numeric)

The most basic regex of all is one that matches a specific alphanumeric character. You can construct such a regex by placing the letter or number of interest between two slashes (`/`).

For example, `/s/` matches the letter `s` anywhere it appears inside a string. It matches `s`, `sand`, `cats`, `cast`, and even `Mississippi`. In this last example, `/s/` matches four times, at each of the occurrences of `s` in the string.

When we say that `/s/` matches four times, we refer specifically to how regex work in Rubular. By default, in most languages, a regex matches each string once or not at all; that is, regex matching is a boolean operation. We won't mention this again until near the end of the book.

Note, however, that `/s/` does not match `S` or `KANSAS`. Regex are case sensitive by default, so if you want to match a capital S, you need to specify `/S/`.

Go ahead and give this a try in Rubular: enter the regex `/s/`, then enter the following strings:

```
s
sand
cats
cast
Mississippi
S
KANSAS

```

Rubular should highlight all the `s` characters in the "Match result" box, thus showing where the regex matches. However, the regex doesn't highlight the uppercase `S` characters; it doesn't match the last two strings. If you change the regex to `/S/`, Rubular should light up all the `S` characters, but not the `s`-es.

Great. This discussion is interesting, but how do you put it to use in a real program? Regex usage in a program is language dependent, and also dependent upon what you need to do. As a starter, though, we can use the `match` method from the Ruby and JavaScript String classes.

**Ruby**

```
str = 'cast'
print "matched 's'" if str.match(/s/)
print "matched 'x'" if str.match(/x/)

```

**JavaScript**

```
var str = 'cast';
if (str.match(/s/)) {
  console.log("matched 's'");
}

if (str.match(/x/)) {
  console.log("matched 'x'");
}

```

Both of these print `matched 's"` since `str` contains the letter `'s'`, and neither prints `matched 'x'` since `str` does not contain the letter `'x'`.

If you aren't acquainted with `match`, you can learn enough with a few minutes of skimming the documentation. We won't use anything more complex than the basic form of `match` that takes a single regex argument and a String caller. You can ignore the rest of the documentation for now.



## [Special Characters](https://launchschool.com/books/regex/read/basic_matching#special)

Regex can also match non-alphanumeric characters. However, some of those have special meaning in a pattern and require specialized treatment. Others have no additional interpretation and need no special treatment.

The following special characters have special meaning in a Ruby or JavaScript regex:

`$ ^ * + ? . ( ) [ ] { } | \ /`

We call such characters *meta-characters*. If you want to match a literal meta-character, you must *escape* it with a leading backslash (`\`). To match a question mark, for instance, use the regex `/\?/`. Go ahead and try `/\?/` now with these strings (and some of your own if you aren't sure what will happen):

Some variants of regex have different meta-characters, and some reverse the sense of escaped characters. In `vim`, for example, `\(` and `\)` are meta-characters, while `(` and `)` match literal parentheses. This reversal can be confusing, but you must be aware of it.

In recent years, programs that use regex have begun to support multiple regex styles. `vim`, for instance now has what it calls *extended syntax* which provides enhanced regex, and also lets you swap the way escaped characters work. You can choose to use `(` and `)` for grouping like most other programs, and use `\(` and `\)` for literal parentheses. Check your documentation to see whether your software supports different syntaxes.

```
?
What's up, doc?
Silence!
"What's that?"

```

You should find that `/\?/` matches all of the question marks in these strings. Try the same strings using `/?/` - you should see an error message instead.

The remaining characters aren't meta-characters; they have no extraordinary meaning inside a regex. Both colons (`':'`) and spaces (`' '`) fall into this category. You can use these characters without an escape since they have no special meaning inside a pattern. For example, try `/:/` against these strings:

```
chris:x:300
A thought; no, forget it.
::::

```

Try changing the regex to `/ /`.

As of this writing, Rubular does not detect a single space as a regex. Try `/[ ]/` instead - this is equivalent to `/ /`, but it works in Rubular.

Now change the regex to `/./` (that's a period between the `/` characters). Whoa! What happened here? Oh, right, `.` is a meta-character; you must escape it. Change the regex to `/\./` instead. That's better now? (We'll return to `/./` and why everything lit up in a later chapter.)



## [Concatenation](https://launchschool.com/books/regex/read/basic_matching#concatenation)

You can *concatenate* two or more patterns into a new pattern that matches each of the originals in sequence. The regex `/cat/`, for instance, consists of the concatenation of the `c`, `a`, and `t` patterns, and matches any string that contains a `c` followed by an `a` followed by a `t`.

Give `/cat/` a try using the following strings:

```
cat
catalog
copycat
scatter
the lazy cat.
CAT
cast

```

If all went well, the first five strings matched the regex, but the last two did not. `CAT` didn't match since it is uppercase, and `cast` didn't match because `s` isn't part of the pattern.

The fact that we use a fancy name like concatenation should give you a hint that more is going on here than meets the eye. The patterns we concatenated are simple; they each match a single, specific character. We aren't limited to these simple patterns though; in fact, you can concatenate any pattern to another to produce a larger regex. There are no practical limits to the number of concatenations you perform other than the physical limitations of your hardware.

This fundamental idea is one of the more important concepts behind regex; patterns are the building blocks of regex, not characters or strings. You can construct complex regex by concatenating a series of patterns, and you can analyze a complex regex by breaking it down into its component patterns.

In theory, your computer's capacity to handle large regex places some limitations on the size and complexity of your regex. In practice, though, your ability to understand and maintain your code places more severe restrictions on it. Your head will reach the breaking point long before your computer does. You'll sometimes hear regex called *write-only expressions* or *line noise* because it's easy to write an unreadable and unmaintainable mess. Use regex not because you can; use them because your code demands them. Often, a bit of refactoring will eliminate the need for a complex regex.



## [Alternation](https://launchschool.com/books/regex/read/basic_matching#alternation)

In this section, we introduce alternation, a simple way to construct a regex that matches one of several sub-patterns. In its most basic form, you write two or more patterns separated by pipe (`|`) characters, and then surround the entire expression in parentheses. For example, try the regex `/(cat|dog|rabbit)/` with the following strings:

```
The lazy cat.
The dog barks.
Down the rabbit hole.
The lazy cat, chased by the barking dog,
dives down the rabbit hole.
catalog
The Yellow Dog
My bearded dragon's name is Darwin

```

As with other patterns, case matters, so the `Dog` in `The Yellow Dog` is not matched.

As with concatenation, there are no built-in restrictions on alternation.

Even though parentheses and pipes are meta-characters that require escaping, we don't do that here. We aren't performing a literal match, but are instead using the "meta" meaning of those characters.

To see the difference, give the regex `/\(cat\|dog\)/` a try with the following strings:

```
(cat|dog)
bird(cat|dog)zebra
cat
dog

```

You'll notice this time that we don't match either `cat` or `dog`; since we escaped everything, the regex matcher looks for literal instances of those characters and doesn't treat them as an alternation operation.



## [Control Character Escapes](https://launchschool.com/books/regex/read/basic_matching#control)

Most modern computing languages use control character escapes in strings to represent characters that don't have a visual representation. For example, `\n`, `\r`, and `\t` are nearly universal ways to represent line feeds, carriage returns, and tabs, respectively. Both Ruby and JavaScript support these escapes, as do all regex engines. For example:

**Ruby**

```ruby
puts "has tab" if text.match(/\t/)

```

**JavaScript**

```javascript
if (text.match(/\t/)) {
  console.log("has tab");
}

```

both print `has tab` if `text` contains a tab character.

```
Note that not everything that looks like a control character escape is a genuine control character escape. For instance:

    \s and \d are special character classes (we'll cover these later)
    \A and \z are anchors (we'll cover these as well)
    \x and \u are special character code markers (we won't cover these)
    \y and \q have no special meaning at all
```



**//i**	i appended after the closing forward slash matches both lowercase and uppercase matches (default is to match case strictly)

**//o**	causes any substitution to occur only once, the first time it is encountered (default is to replace all occurrences)

**//m**	makes the dot match newlines (default is to match any character except newline, i.e., '\n'; other languages use /s for this)

**//x**	tells Ruby to ignore whitespace between regex tokens

https://www.regular-expressions.info/ruby.html



### Examples:

**/,|[ ]/**	matches a comma (,) or a space ([ ]) 

**/(blue|black)berry/**	looks for '-berry' concatenated with a prefix of either 'blue' or 'black'



## Character Classes

**character classes**	patterns that let you specify a set of characters that you want to match, enclosed by brackets ([]).

**Set of Characters**

/[FX]/ 	looks for all occurrences of 'F' or 'X'

/[e+]/	finds all occurrences of 'e' or '+'

Character class patterns come in handy in all kinds of situations. For example, if a program wants a user to choose between five different options by entering a number between 1 and 5, you can validate that input with the regex `/[12345]/`. Likewise, you can validate a `y/n` prompt response with `/[nyNY]/`

Single-character classes (e.g., `/[a]/`) are possible and 
even useful, though we won't get into that here. Don't automatically remove the brackets if you encounter one in code you're working on: it's probably there for a reason.

Character classes also come in handy when you need to check for uppercase and lowercase letters, but can't use the `i` flag to make the entire regex case insensitive. For example, `/[Hh]oover/` matches `Hoover` or `hoover`, but not `HOOVER`.

**Meta-characters in character classes** are fewer:

​	^ \ - [ ]

`[^]`	**not** whatever follows the carat symbol

​	`You can escape any of the special characters, even if you don't have to. Thus, `/[\*\+]/` is an acceptable, albeit less readable, equivalent to `/[*+]/`. As before, though, you should keep this list of class meta-characters handy until you know it by heart.

`/[0-9A-Fa-f][0-9A-Fa-f][0-9A-Fa-f]/`	matches a 3-digit hexadecimal code

`[^aeiou]`	matches anything but 'a', 'e, 'i', 'o' or 'u'

```ruby
text = 'xyx'
puts 'matched' if text.match(/[^x]/)
# matched  ([^x] matches the y, which is truthy)
```

Why is that? Rubular (and Scriptular) show you which characters match each regex; what it doesn't show explicitly is that `match` returns a truthy value when there is a match anywhere in the string. Though Rubular shows `/[^x]/` matching the `y` in `xyx` and nothing else, `text.match` is still truthy.

**Examples:**

`/[kKs]/`		matches 'K', 'k' or 's'

`/[bc][aou]t/i`	matches lowercase or uppercase variants of any of the words 'cat', 'cot', 'cut', 'bat', 'bot', 'but'; READ:  begins with 'b' or 'c', followed by 'a', 'o' or 'u', followed by 't', lowercase or uppercase

`/0-9a-j]/i`	matches 0-9 and lowercase or uppercase a-j

`/A-WYZa-wyz/`	matches all letters except x or X

`/[^a-z]i`	matches any character that isn't a lowercase or uppercase letter

```ruby
/\[\^[0-9A-Za-z]-[0-9A-Za-z]\]/
# or
/[\[][\^][0-9A-Za-z]-[0-9A-Za-z][\]]/
```

There are six patterns in these regexes:

| Pattern        | Explanation                                            |
| -------------- | ------------------------------------------------------ |
| `\[` or `[\[]` | a literal `[`                                          |
| `\^` or `[\^]` | a literal `^`                                          |
| `[0-9A-Za-z]`  | any of the usual character class range starting values |
| `-`            | a literal '-'                                          |
| `[0-9A-Za-z]`  | any of the usual character class range ending values   |
| `\]` or `[\]]` | a literal `]`                                          |



## Character Class Shortcuts

Regexes include shortcuts to commonly-used character classes.  These can be used in or out of square brackets.

### Shortcuts

`/./`	any character

`/./m`	any character, including \n (newline)

`/\s/`	any whitespace character, equivalent to `/[ \t\v\r\n\f]/`

​			\t tab, \v vertical tab, \r carriage return, \n newline, \f form feed		

`/\S/`	any non-whitespace character, equivalent to `/[^\t\v\r\n\f]/`

\d		any decimal digit (0-9)

\D		any character but a decimal digit

\h		any hexadecimal digit (0-9, A-F, a-f)

\H		any character except a hexadecimal digit

\w		any 'word characters', i.e., `[a-zA-Z0-9_]`

\W		any non-word characters, i.e., `[^a-zA-Z0-9_]`



Examples:

`/\s...\s/`	any 3 characters delimited by whitespace

`/\s\h\h\h\h\s/`	any 4-digit hex number delimited by whitespace

'/[a-z][a-z][a-z]/i'	any sequence of three letters, uppercase or lowercase





## Anchors

Anchors provide a way to limit how a regex matches a particular string by telling the regex engine where matches can begin and where they can end.  What they do is ensure that a regex matches a string at a specific  place: the beginning or end of the string or end of a line, or on a word or non-word boundary.

^	beginning of a line

$	end of a line

\A	beginning of a string

\Z 	end of a string (not including \n)

\z 	end of a string (including \n); use this until you determine you need \Z

\b	word boundaries; words are sequences of word characters (\w)

​	*A word-boundary occurs:*

-   between any pair of characters, one of which is a word character and one which is not.
-   at the beginning of a string if the first character is a word character.
-   at the end of a string if the last character is a word character.

	B 	non-word boundaries (\W)

			*A non-word boundary occurs:*

-  between any pair of characters, both of which are word characters or both of which are not word characters.
-   at the beginning of a string if the first character is a non-word character.
-   at the end of a string if the last character is a non-word character.



Word boundaries:

```plaintext
Eat some food.
```

Here, word boundaries occur before the `E`, `s`, and `f` at the start of the three words, and after the `t`, `e`, and `d` at their ends. Non-word boundaries occur elsewhere, such as between the `o` and `m` in `some`, and following the `.` at the end of the sentence.

To anchor a regex to a word boundary, use the `\b` pattern. For example, to match 3 letter words consisting of "word characters", you can use `/\b\w\w\w\b/`. Try it with:

```plaintext
One fish,
Two fish,
Red fish,
Blue fish.
123 456 7890
```

It's rare that you must use the non-word boundary anchor, `\B`. Here's a somewhat contrived example you can try. Try the regex `/\Bjohn/i` against these strings:

```plaintext
John Silver
Randy Johnson
Duke Pettijohn
Joe_Johnson
```

The regex matches `john` in the last two strings, but not the first two.

`\b` and `\B` do not work as word boundaries inside of character classes (between square brackets). In fact, `\b` means something else entirely when inside square brackets: it matches a backspace character.



Examples:

`/^cat/`	matches 'cat' at the beginning of a line

`/cat$/`	matches 'cat' at the end of a line

`/^cat$/`	matches 'cat' at both the beginning and the end of a line (by itself, essentially, on a line)

`/\b\w\w\w\b/`	matches three word characters delimited by word boundaries

`/\Bjohn/i`	matches 'john' uppercase or lowercase, if it occurs after a non-word boundary ex. -- 'Joe_Johnson' or 'Duke Pettijohn'

`/^The\b/`	matches the word 'The' at the beginning of a line

`/\bcat$/`	matches the word 'cat' at the end of a line

`/\b[a-z][a-z][a-z]\b/i`	matches any three-letter word, lowercase or uppercase

`/\b(A|The)\b[ ][a-zA-Z][a-zA-Z][a-zA-Z][a-zA-Z][ ](dog|cat)$/`	matches 'A' or 'The' followed by a space, then any 4 letters, lowercase or uppercase, a space and finally 'dog' or 'cat'

A proper Ruby solution, using \A and \z instead of ^ $ for this looks like:

`/A(A|The) [a-zA-Z][a-zA-Z][a-zA-Z][a-zA-Z] (dog|cat)z/`



As we mentioned above, there's some subtlety involved with how `^` and `$` work in Ruby. This subtlety arises when the string you are attempting  to match contains one or more newline characters that aren't the last  character in the string. For example, consider this code:

```ruby
TEXT1 = "red fish\nblue fish"
puts "matched red" if TEXT1.match(/^red/)
puts "matched blue" if TEXT1.match(/^blue/)
# => matched red
# => matched blue
```

This example outputs both `matched red` and `matched blue` since `^` anchors the regex to the beginning of each line in the string, not the beginning of the string. 

```ruby
TEXT2 = "red fish\nred shirt"
puts "matched fish" if TEXT2.match(/fish$/)
puts "matched shirt" if TEXT2.match(/shirt$/)
# => matched fish
# => matched shirt
```

As before, we get a match for both regex. 

```ruby
TEXT3 = "red fish\nblue fish"
TEXT4 = "red fish\nred shirt"
puts "matched red" if TEXT3.match(/\Ared/)
puts "matched blue" if TEXT3.match(/\Ablue/)
puts "matched fish" if TEXT4.match(/fish\z/)
puts "matched shirt" if TEXT4.match(/shirt\z/)
# => matched red
# => matched shirt
```

```
Even though we recommend using `\A` and `\z` for most anchored matches in Ruby, most examples and exercises in this book use `^` and `$` instead. It is easier to demonstrate certain behaviors when using `^` and `$` on Rubular.
```





## Quantifiers

`/x*/`	matches 'x' and all spaces between characters in any string (matches between every character)



### Zero or More

`*`	matches zero or more occurrences of the pattern to its left



Examples:

`/\b\d\d\d\d*\b/`	match 3 consecutive digits beginning at a word boundary, followed by any number of digits and then another word boundary

`/co*t/`	matches a 'c', followed by any number (or no) 'o's, followed by a 't', i.e., 'ct', 'cot', 'coot', etc.

`/1(234)*5/`	matches a '1' followed by any number of repetitions of '234' and then a '5', i.e., 12345, 15, 12342345, etc.



### One or More

`+`	match 1 or more occurrences of the pattern to its left



Examples:

`/\b\d\d\d\d+\b/`	matches 4 or more consecutive digits beginning at and ending at word boundaries



### Zero or One

`?`	match 0 or 1 occurrence of the pattern to its left



Examples:

`/coo?t/`	matches a 'c' followed by an 'o'  followed by an optional 'o' and finally a 't', i.e., 'cot' or 'coot'

One place you might use a `?` would be a pattern where you are trying to match a date whose components may or may not include `-` separator characters. For instance, you have dates formatted as both `20170111` or `2017-01-11`. To match such dates, you can use the regex `/\b\d\d\d\d-?\d\d-?\d\d\b/`. This matches:

```plaintext
20170111
2017-01-11
2017-0111
201701-11
```

but not:

```plaintext
2017/01/11
```



### Ranges

`p{m}`	matches precisely `m` occurrences of the pattern `p`

`p{m,}`	matches `m` or more occurrences of `p`

`p{m,n}`	matches `m` or more occurrences of `p`, but not more than `n`



Examples:

`/\b\d{10}\b/`	matches ten consecutive digits delimited by word boundaries

`/\b\d{3,}\b/`	matches numbers that are at least 3 digits long

`/\b[a-z]{5,8}\b/i`	matches words of 5 to 8 letters, lowercase or uppercase



### Greediness

The quantifiers we've discussed thus far are **greedy**: they always match the longest possible string they can.  For instance, try matching `/a[abc]*c/` against `xabcbcbacy`.  You should see that this pattern matches `abcbcbac`, not `abc` or `abcbc` both of which could match the pattern, but are shorter than the final  match string. This aspect of regex isn't often a concern, but when it  is, it can be highly confusing if you aren't familiar with greediness.

In most cases, greediness is what you want. However, sometimes it isn't, and you need to match the fewest number of characters possible; we call this a **lazy** match. In Ruby and JavaScript, you can request a lazy match by adding a `?` after the main quantifier. For example, `/a[abc]*?c/` matches `abc` and `ac` in `xabcbcbacy`.



Exercises:

`/\bb[a-z]*e\b/`	matches any word beginning with 'b' and ending with 'e' and having any number of letters in-between

`/^.*\?$`/		matches any line of text that ends with a '?'

(`.*`is how you ignore everything between two points when matching)

`/^.+\?$/`	matches any line of text that ends with a '?' and has at least one character before it

`/^https?:\/\/\S*$/`	matches a line of text that contains nothing but a URL (http or https), ending with a whitespace character or end of line

`/^\s*https?:\/\/\S*\s*$/`	matches a line of test that contains nothing but a URL (http or https), ending with a whitespace character or end of line, delimited optionally by whitespace

`/\bhttps?:\/\/\S*/`	matches a URL anywhere on a line which begins with a word boundary



`/\b[a-z]*i[a-z]*i[a-z]*i[a-z]*\b/i` or `/\b([a-z]*i){3}[a-z]*\b/i`

matches any word which contains at least three 'i's



`/[a-z]*\S$/`	or  `/\S+$/`

matches the last word in each line of text (any sequence of non-whitespace characters)



`/^,(\d+,){3,6}$/`	matches lines of 3 to 6 comma-separated numbers of any length



`/^(\d+),(\d+,){1,4}(\d+)$/` or `/^(\d+,){2,5}\d+$/`

matches lines of 3 to 6 comma-separated numbers without commas at the beginning or end of the line (just between the numbers)


`/<(H|h)1>.*?<\/(H|h)1>/`	matches any pair of h1 HTML tags, including what's inside them; we use a lazy quantifier here (`.*?`) instead of the default greedy quantifier (`.*`) in order to avoid picking up other tag sets between sets of h1 tags, i.e., to avoid also selecting the p tag in the example: <h1>ABC</h1> <p>Paragraph</p> <h1>DEF</h1><p>Done</p>

​	



## Using Regular Expressions in Ruby and JavaScript

Ruby's `Regexp` class doesn't provide the regex methods most often used.  Instead, the `String` class does.

### Matching Strings

`match` returns a truthy value indicating whether a match occurred and what substrings matched.  It is used at its most basic like this:

**Ruby**

```ruby
fetch_url(text) if text.match(/\Ahttps?:\/\/\S+\z/)
```

**JavaScript**

```javascript
if (text.match(/^https?:\/\/\S+$/)) {
  fetch_url(text);
}
```

Here we call `fetch_url(text)` when `match` returns a value that indicates a match: that is when `text` contains something that looks like a URL.

`match` returns an Array that contains the string we matched  against, along with the capture groups defined in the regex. If we name  this Array `capture`, then `capture[0]` represents the entire matched portion of `text`, while `capture[1]`, `capture[2]`, etc. correspond to the capture groups. (We discuss capture groups below.). If the regex doesn't match `text`, then Ruby returns `nil`, while JavaScript returns `null`.

```
In Ruby, the return value of match isn't an Array, but a MatchData object that responds to [0], [1], [2], and so on. You cannot apply most Array methods to this object directly.
```

```
In Ruby, you sometimes see something like this:

		fetch_url(text) if text =~ /\Ahttps?:\/\/\S+\z/

=~ is similar to match, except that it returns the index within the string at which the regex matched, or nil if there was no match. =~ is measurably faster than match, so some rubyists prefer to use it when they can. Others dislike it because it is unfamiliar, or solely because =~ reminds them of the Perl language where it saw widespread use.

```

Rubyists should also investigate the `String#scan` method; it is a global form of `match` that returns an Array of all matching substrings.



### [Splitting Strings](https://launchschool.com/books/regex/read/using#split)

Applications that process text often must analyze data comprised of  records and fields delimited by some special characters or delimiters. A typical format has records separated by newlines, and fields delineated by tabs. Such data often needs parsing before you can use it in your  program; the `split` method is an often-useful parsing tool.

`split` is frequently used with a simple string as a delimiter:

**Ruby**

```ruby
record = "xyzzy\t3456\t334\tabc"
fields = record.split("\t")
# -> ['xyzzy', '3456', '334', 'abc']
```

**JavaScript**

```javascript
var record = "xyzzy\t3456\t334\tabc";
var fields = record.split("\t");
// -> ['xyzzy', '3456', '334', 'abc']
```

As you can see, `split` returns an `Array` that contains the values from each of the split fields.

Not all delimiters are as simple as that, though. Sometimes,  formatting is much more relaxed. For example, you may encounter data  where arbitrary whitespace characters separate fields, and there may be  more than one whitespace character between each pair of items. The regex form of `split` comes in handy in such cases:

**Ruby**

```ruby
record = "xyzzy  3456  \t  334\t\t\tabc"
fields = record.split(/\s+/)
# -> ['xyzzy', '3456', '334', 'abc']
```

**JavaScript**

```javascript
var record = "xyzzy  3456  \t  334\t\t\tabc";
var fields = record.split(/\s+/);
// -> ['xyzzy', '3456', '334', 'abc']
```

```
Beware of regex like /:*/ and /\t?/ when using split. Recall that the * quantifier matches zero or more occurrences of the pattern it is modifying. In the case of split, the result may be totally unexpected:

		'abc:xyz'.split(/:*/)
		# -> ['a', 'b', 'c', 'x', 'y', 'z']

A six element array instead of the two element array you may have expected. This result occurs because the regex matches the gaps between each letter; zero occurrences of : occurs between each pair of characters.
```



### [Capture Groups: A Diversion](https://launchschool.com/books/regex/read/using#captures)

Note that regex also have **non-capture groups** but we won't cover them here.

You've already encountered these before, though we called them something different at the time: grouping parentheses. We didn't mention it at  the time, but these meta-characters have another function: they provide  capture and non-capture groups.

Capture groups capture the matching characters that correspond to part  of a regex. You can reuse these matches later in the same regex, and  when constructing new values based on the matched string.

We'll start with a simple example. Suppose you need to match quoted  strings inside some text, where either single or double quotes delimit  the strings. How would you do that using the regex patterns you know?  You might consider:

```ruby
/['"].+?['"]/
```

as your first attempt to match quotes, but, you'll soon find that it  also matches mixed single and double quotes. This may not be what you  want. Instead, you need a way to capture the opening quote and reuse  that character for the closing quote. It's time to call on capture  groups:

```ruby
/(['"]).+?\1/
```

Here the group captures the part of the string that matches the pattern  between parentheses; in this case, either a single or double quote. We  then match one or more of any other character and end with a `\1`: we call this sequence a **backreference** - it references the first capture group in the regex. If the first group matches a double quote, then `\1` matches a double quote, but not a single quote.

```
It may be more reasonable to use two regex to solve this problem:

if text.match(/".*?"/) || text.match(/'.*?'/)
  puts "Got a quoted string"
end

It's easier to read and maintain when written like this. However, you will almost certainly encounter problems where a single regex with a backreference is the preferred solution.
```

A regex may contain multiple capture groups, numbers from left to right  as groups 1, 2, 3, and so on, up to 9. As you might expect, the  backreferences are `\1`, `\2`, `\3`, ..., and `\9`.

```
Note that there are patterns in Ruby that allow for named groups and named backreferences, but this is beyond the scope of this book. If you find yourself needing multiple groups in Ruby regex, you may want to investigate these named groups and backreferences.
```

**Capture groups** are most useful in conjunction with methods that use regex to transform strings. We'll see this in the next two sections.



### [Transformations in Ruby](https://launchschool.com/books/regex/read/using#trans-ruby)

`()`	a **capture group**, which captures the part of the string that matches the pattern between parentheses

`\1`	a **backreference**, which refers to whatever matched a **capture group** (you can have multiple with ascending numerical values, i.e., \1, \2, \3, etc.)

While regex-based transformations in Ruby and JavaScript are  conceptually similar, the implementations are different. We'll cover  these transformations in separate sections.

Transforming a string with regex involves matching that string  against the regex, and using the results to construct a new value. In  Ruby, we typically use `String#sub` and `String#gsub`. `#sub` transforms **the first part of a string that matches** a regex, while `#gsub` **transforms every part of a string that matches**.

Here's a simple example:

```ruby
text = 'Four score and seven'
vowelless = text.gsub(/[aeiou]/, '*')
# -> 'F**r sc*r* *nd s*v*n'
```

Here we replace every vowel in `text` with an `*`.

We can use backreferences in the replacement string (the second argument):

```ruby
text = %(We read "War of the Worlds".)
puts text.sub(/(['"]).+\1/, '\1The Time Machine\1')
# prints: We read "The Time Machine".
```

One thing to note here is that if you double quote the replacement string, you need to double up on the backslashes:

```ruby
puts text.sub(/(['"]).+\1/, "\\1The Time Machine\\1")
```

When possible, try to use single quotes to avoid **leaning toothpick syndrome**.



### [Transformations in JavaScript](https://launchschool.com/books/regex/read/using#trans-js)

While regex-based transformations in Ruby and JavaScript are  conceptually similar, the implementations are different. We'll cover  these transformations in separate sections.

Transforming a string with regex involves matching that string  against the regex, and using the results of the match to construct a new value. In JavaScript, we can use the `replace` method which transforms the matched part of a string. If the regex includes a `g` option, the transformation applies to every match in the string.

Here's a simple example:

```javascript
var text = 'Four score and seven';
var vowelless = text.replace(/[aeiou]/g, '*');
// -> 'F**r sc*r *nd s*v*n'
```

Here we replace every vowel in `text` with an `*`. We applied the transformation globally since we used the `g` option on the regex.

We can use backreferences in the replacement string (the second argument):

```javascript
var text = 'We read "War of the Worlds".';
console.log(text.replace(/(['"]).+\1/, '$1The Time Machine$1'));
// outputs: We read "The Time Machine".
```

One thing to note here is that the backreferences in the replacement string use `$1`, `$2`, etc. instead of `\1`, `\2`, etc.
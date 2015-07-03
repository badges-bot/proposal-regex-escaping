## List of Escaped Characters

This file contains a list of escaped characters under this proposal. Each character details the reason it is escaped.

### `SyntaxCharacter` Proposal

This proposal is currently the primary proposal and escapes characters under the `SyntaxCharacter` class 
in the ES2015 specification. The characters included in the list are the following:

|Character  | Why escape it?
|-----------|--------------|
| `^`       | So that `new RegExp(RegExp.escape('^') + "a")` will match `"^a"` rather than the `^` being treated as a negation or start of sentencecontrol construct. | 
| `$`       | So that `new RegExp("a" + RegExp.escape('$'))` will match `"a$"` rather than the `$` being treated as a end of sentence control construct. | 
| `\`       | So that `new RegExp(RegExp.escape("\\"))` won't throw a type error and instead match `"\\"`, and more generally that `\` won't be treated as an escape control construct. |
| `.`       | So that `new RegExp(RegExp.escape("."))` won't be matched against single characters like `"a"` but instead against an actual dot ("."), and more generally that `.` won't be treated as an "any character" control construct. |
| `*`       | So that `new RegExp(RegExp.escape("*"))` won't throw a type error but instead match against an actual star ("*"), and more generally that `*` won't be treated as a "zero or more times" quantifier. |
| `+`       | So that `new RegExp(RegExp.escape("+"))` won't throw a type error but instead match against an actual plus sign ("+"), and more generally that `+` won't be treated as a "one or more times" quantifier. |
| `?`       | So that `new RegExp(RegExp.escape("?"))` won't throw a type error but instead match against an actual question mark sign ("?"), and more generally that `?` won't be treated as a "once or not at all" quantifier. |
| `(`       | So that `new RegExp(RegExp.escape("("))` won't throw a type error but instead match against an actual opening parenthesis  ("("), and more generally that `(` won't be treated as a "start of a capturing group" logical operator. |
| `)`       | So that `new RegExp(RegExp.escape(")"))` won't throw a type error but instead match against an actual closing parenthesis  (")"), and more generally that `(` won't be treated as a "end of a capturing group" logical operator. |
| `[`       | So that `new RegExp(RegExp.escape("["))` won't throw a type error but instead match against an actual opening bracket ("["), and more generally that `[` won't be treated as a "start of a character class" construct. |
| `]`       | This construct is needed to allow escaping inside character classes. `new RegExp("]")` is perfectly valid but we want to allow `new RegExp("["+RegExp.escape("]...")+"]")` in which the `]` needs to be taken literally (and not as the closing "end of character class" character.  |
| `{`       | So that `new RegExp("a" + RegExp.escape("{1,2}"))` will not match `"aaa"`, and more generally that `{` is taken literally and not as a quantifier. | 
| `}`       | So that `new RegExp("a" + RegExp.escape("{1,2}"))` will not match `"aaa"`, and more generally that `}` is taken literally and not as a quantifier. | 
| `|`       | So that `|` will be treated literally and `new RegExp(Regxp.escape("a|b"))` will produce a string that matches `"a|b"` instead of the | being treated as a logical "or" operator. |


### "Safe with extra escape set" Proposal.

This proposal additionally escapes `-` for context sensitive inside-character-class matching, hex numeric literals (0-9a-f) at the start of the string in order to avoid hitting matching groups and lookahead/lookbehind control characters.

TODO(benjamingr) add reasoning for "safe with extra set" characters here.

### Extended "Safe" Proposal

This proposal escapes a maximal set of characters and ensures compatibility with edge cases like passing the result to `eval`.

TODO(benjamingr) add reasoning for "safe" characters here
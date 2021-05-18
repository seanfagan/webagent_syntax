# WebAgent Syntax
WebAgent syntax highlighting in Sublime. Work-in-progress!

## Installation
todo

## Contributing
### Installing for development
In Sublime, open Preferences > Browse Packages. This should open your file explorer to the Sublime directory for packages. Open the default "User" package directory. Download the .sublime-syntax file(s) into here.

### Word boundaries in WebAgent
A "word boundary" is the boundary between a word character and a non-word character. RegEx has a symbol for word boundaries, `\b`. RegEx considers these characters to be "word characters": `a-z, A-Z, 0-9, _`. In webAgent, the hyphen should also be considered a word character (it's used the same way an underscore is used). Since webAgent's word characters differ from RegEx, we can't use rely on `\b` to find word boundaries.

To find word boundaries in webAgent, we use lookaheads and lookbehinds that include hyphens as word characters:
```
# ADD keyword
- match: (?i)(?<![\w-])add(?![\w-])
```
1. `(?i)` modifies the mode of RegEx to be case-insensitive.
2. `(?<![\w-])` is a negative lookbehind that will discard a result if it's preceded by any of these characters: `a-z, A-Z, 0-9, _, -`. E.G. `#VARIABLE-TO-ADD` will not match `ADD` because it's preceded by a hyphen.
3. `add` is the main expression of what to match.
4. `(?![\w-])` is a negative lookahead that will discard a result if it's followed by any of these characters: `a-z, A-Z, 0-9, _, -`. E.G. `#ADD-VARIABLE` will not match `ADD` because it's followed by a hyphen.

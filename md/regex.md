# Cheat sheet: RegEx

## Main syntax

- \d - any digit
- \b - boundary
- \w - any characters
- \s - any space
- \D - not a digit
- \W - not a character
- \S - not a space
- "." - any character except for a new line
- "+" - one or occurrences
- "+?" - one or more occurrences
- "*" - zero or more occurrence
- "?" - zero or one occurrence
"/abc/" - a sequence of characters
"[abc]" - any character from a set of characters
"[^abc]" - any character not a set of characters
"[a-z]" - any characters in a range of characters
"a{5,7}" - five to sever occurrences of character
"a{5,}" - from five to infinite occurrences
"(abc)" - group
"a|b|c" - any of patterns
"^" - start of input
"$" - end of input

## Useful JavaScript RegEx native methods

```javascript
//  test()
const pattern = /test/gi;
const str = 'Is this is a test?';
pattern.test(str); // true

//  match()
const paragraph = 'The quick brown fox jumps over the lazy dog. It barked.';
const regex = /[A-Z]/g;
const found = paragraph.match(regex);
console.log(found); // expected output: Array ["T", "I"]

//  search()
const paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';
// any character that is not a word character or whitespace
const regex = /[^\w\s]/g;
console.log(paragraph.search(regex)); // expected output: 43
console.log(paragraph[paragraph.search(regex)]);  // expected output: "."

//  exec()
const regex = RegExp('test', 'gi');
const str = 'Is this is a test?';
console.log(regex.exec(str)); //  [ 'test', index: 13, input: 'Is this is a test?', groups: undefined ]

```

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
- "\*" - zero or more occurrence
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
const paragraph =
  'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';
// any character that is not a word character or whitespace
const regex = /[^\w\s]/g;
console.log(paragraph.search(regex)); // expected output: 43
console.log(paragraph[paragraph.search(regex)]); // expected output: "."

//  exec()
const regex = RegExp('test', 'gi');
const str = 'Is this is a test?';
console.log(regex.exec(str)); //  [ 'test', index: 13, input: 'Is this is a test?', groups: undefined ]
```

## Usefaul RegEx's

Simple password

> /^.{4,16}$/gi

Latin/Cyrillic name with dash

> /^[A-ZА-ЯЁ][a-zA-Zа-яёА-ЯЁ]+(?:[-][a-zA-Zа-яёА-ЯЁ]+)\*$/u

Phone

> /^[+]?[(]?[0-9]{3}[)]?[-\s.]?[0-9]{3}[-\s.]?[0-9]{4,6}$/

Phone

> /^((\+[1-9]{1}[ -]?)|(\([0-9]{3}\)[ -]?)|([0-9]{3})[ -]?)\*?[0-9]{2}[ -]?[0-9]{2}$/

Simple email

> /\S+@\S+\.\S+/

Only latin email

> /(?:[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)_|"")@(?:(?:[a-z0-9](?:[a-z0-9-]_[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:(2(5[0-5]|[0-4][0-9])|1[0-9][0-9]|[1-9]?[0-9]))\.){3}(?:(2(5[0-5]|[0-4][0-9])|1[0-9][0-9]|[1-9]?[0-9])|[a-z0-9-]\*[a-z0-9])\])/

Simple ru date

> /\d{2}[.]\d{2}[.]\d{4}/

Ru date

> /(^0[1-9]|[12][0-9]|3[01]).(0[1-9]|1[0-2]).(\d{4}$)/;

Forbidden symbols for strings

> /[`~!@#$%^&\*()\_|+=?;:'",.<>{}[\]\\/]/gi

IPv4

> /\b((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)(\.|$)){4}\b/

Coords

> /^\d+(\.\d+)?$/

Time

> /^([0-1][0-9]|[2][0-3]):([0-5][0-9])$/

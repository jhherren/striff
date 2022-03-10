# striff

Simple string diffing. Given two strings, `striff` will return an object noting which characters were added or removed, and at which indices.

## Installation

Run `npm install striff`. Or stick in on a page [via CDN](https://unpkg.com/striff).

## Usage

Import it, pass a couple of strings, and do whatever you want with the results.

```js
import striff from "striff";

const result = striff("string #1", "string #2");

// {
//   added: [
//     ...added characters
//   ],
//   removed: [
//     ...removed characters
//   ]
// }
```

## Examples

Here's the kind of result you'll get with different types of diffing.

### Strings w/ Characters Added

```js
const str1 = "abc";
const str2 = "abcde";

const result = striff(str, str2);
```

#### Result

```js
{
  added: [
    {
      character: "d",
      index: 3
    },
    {
      character: "e",
      index: 4
    }
  ],
  removed: []
}
```

### Strings w/ Characters Removed

```js
const str1 = "abc";
const str2 = "a";

const result = striff(str, str2);
```

#### Result

```js
{
    added: [],
    removed: [
    {
      character: "b",
      index: 1
    },
    {
      character: "c",
      index: 2
    }
  ]
}
```

### Strings w/ Duplicate Characters

Handling strings with duplicate, consecutive characters removed is a little weird. For strings whose characters were changed at the _end_, the indices will be grouped together at the end of the string.

```js
const str1 = "abbbc";
const str2 = "ab";

const result = striff(str, str2);
```

#### Result

```js
{
  added: [],
  removed: [
    {
      character: "b",
      index: 2
    },
    {
      character: "b",
      index: 3
    },
    {
      character: "c",
      index: 4
    }
  ]
}
```

For those whose whose characters were changed at the _beginning_, the indices will be grouped together at the beginning.

```js
const str1 = "abbbc";
const str2 = "bc";

const result = striff(str, str2);
```

#### Result

```js
{
  added: [
    {
      character: "b",
      index: 0
    },
    {
      character: "b",
      index: 1
    },
    {
      character: "c",
      index: 2
    }
  ],
  removed: []
}
```

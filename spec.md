# CompactData Specification
<!-- vscode-markdown-toc -->
<!-- 1. [Introduction](#Introduction)
2. [Status](#Status)
3. [Rules](#Rules)
4. [Values](#Values)
	- 4.1. [Map](#Map)
	- 4.2. [Array](#Array)
	- 4.3. [Pair](#Pair)
		- 4.3.1. [Standard Pair](#StandardPair)
		- 4.3.2. [Map Pair](#MapPair)
		- 4.3.3. [Array Pair](#ArrayPair)
		- 4.3.4. [Orphan Pairs](#OrphanPairs)
	- 4.4. [Number](#Number)
	- 4.5. [String](#String)
	- 4.6. [Boolean](#Boolean)
	- 4.7. [Null](#Null)
5. [Type Inference](#TypeInference)
6. [Quoting Values](#QuotingValues)
7. [Escaping](#Escaping)
8. [Encoding For DNS](#EncodingForDNS)
	8.1. [Hex Values](#HexValues)
9. [Reserved Characters](#ReservedCharacters) -->

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

* auto-gen TOC
{:toc}

## Introduction

CompactData is a data serialisation format with the goal of describing objects in as few characters as possible. CompactData has particular application in DNS TXT records because:

- it is character-efficient
- it is easily minified
- keys and values do not need to be "quoted" – avoiding DNS storage issues

Until now, developers have rolled their own methods of storing data in DNS TXT records, presenting significant limitations and a barrier to entry for those looking to store data in DNS. CompactData aims to standardise data storage in DNS TXT.

## Status
We do not anticipate any changes to the grammar or parser rules.

## Rules
- Whitespace means space (`0x20`) or tab (`0x09`).
- Newline means `LF` (`<0x0A`) or `CRLF` (`0x0D0A`).
- CompactData ignores all leading and trailing whitespace.
- CompactData files must be valid UTF-8 encoded Unicode documents.

## Values
Values are described precisely below:

### Map
A map begins with left parenthesis `(` and ends with right parenthesis `)`, it contains zero or more pairs separated by a semi-colon (`;`).

```
(
  a=1;
  b=2;
  c=3
)
```

### Array
Arrays in CompactData will be familiar to most – beginning with a left square bracket `[` and ending with a right square bracket `]` containing zero or more values separated by a semi-colon `;`. Array items can be of any data type and data types can be mixed.

```
[
  1;
  2;
  3
]
```

### Pair
Pairs are the primary building block of CompactData and consist of a value assigned to a key. They can be used in a number of ways to aid character efficiency. Orphan pairs (not within a map) are allowed for character efficiency and are converted into a map when parsed.

#### Standard Pair
A standard pair is a key and a value separated by equals (`=`):

```
(
  a=1
)
```

#### Map Pair
When assigning a map to a key, we can omit `=` since the left parenthesis separates the key from the map contents:

```
(
  a(
    b=1
  )
)
```

#### Array Pair
When assigning an array to a key, we can omit `=` since the left square bracket separates the key from the array contents:

```
(
  a[
    1;
    2
  ]
)
```

#### Orphan Pairs
An orphan pair is one that is expressed outside of a map, either at the top level of an object or as an array value.

##### At the top level
Pairs can be expressed outside of a map at the top level and they are automatically considered pairs in the same map:

```
a=1;
b=2;
c=3
```

##### As array values
Pairs can be expressed as values in an array, where they are automatically considered individual maps each with one pair:

```
[
  a=1;
  b=2;
  c=3
]
```

### Number
Numbers in CompactData are the same as numbers in JSON [view RFC](https://tools.ietf.org/html/rfc7159#section-6).

### String
Strings in CompactData are the same as strings in JSON [view RFC](https://tools.ietf.org/html/rfc7159#section-7), with the exception that they can also be unquoted and `` `graved` ``.

### Boolean
True is represented using `true` and false is represented using `false` – in both cases, the same as JSON.

### Null
Null is represented using `null`, the same as JSON.

## Type Inference
CompactData infers the type of a value, to set a number to a string it can be quoted. For example:

```
(
  force_number_as_string="1"
)
```

## Quoting Values
Values can be quoted using double quotes (`"`) or DNS-friendly graves (`` ` ``), for example:

```
(
  force_number_as_string="1";
  force_another_number_as_string=`2`
)
```

## Escaping
Like JSON, the backslash (`\`) can be used to escape characters. In addition, the DNS-friendly tilde (`\~`) can also be used as an escape character. For character efficiency, it's usually better to quote values that include more than one reserved character. For example:

```
(
  include_one_reserved_char = we won :\);
  include_many_reserved_chars = "this (that [the other]"
)
```
In CompactData tilde (`\~`) is equivalent to backslash (`\`). Backslash can be used to escape tilde and tilde can be used to escape backslash. Tilde can be used to escape tilde. Backslash can be used to escape backslash.

## Encoding For DNS
CompactData is not limited to [ASCII characters](https://en.wikipedia.org/wiki/ASCII) but some storage media are (e.g. DNS TXT records). Non-ASCII characters can be expressed in ASCII CompactData in two ways:

### Hex Values
Any unicode character represented by four hex digits can be used in CompactData in the same way as JSON:

```
(
  symbol=\u03C0
)
```

A DNS-friendly version is also available using the tilde (`\~`) in place of the back slash (`\`):

```
(
  symbol=~u03C0
)
```

## Reserved Characters
For character efficiency, you should use a quoted or graved string if a value includes two or more reserved characters, otherwise use an escape character (`\` or `\~`) for a single reserved character. The following characters have special meaning in CompactData:

- **Brackets**: The left bracket `(` indicates the start of a map, the right bracket `)` indicates the end.
- **Square Brackets**: The left square bracket `[` indicates the start of an array, the right square bracket `]` indicates the end.
- **Semi-colon** `;` is used in a <<map,map>> to separate <<pair,pairs>> and used in an <<array,array>> to separate items.
- **Grave accents and double quotes** (`` ` `` and `"` respectively) are used for <<quoting_values,quoting values>>
- **Backslash and tilde** (`\` and `~` respectively) are escape characters and can be used before any reserved character to escape its reserved use. To use a backlash or tilde in a CompactData object, simply use two: `\\`, `~~`, `\~` or `~\`.

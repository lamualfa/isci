# ISCI Draft-1

Release on **7 Feb 2020**

## List Contents

- [JSON Schema](#json-schema)
- [ISCI Formats](#isci-formats)
- [Available Keyword Types](#available-keyword-types)
  - [randCharset](#randcharset)
  - [incrNumber](#incrnumber)
  - [incrCharset](#incrcharset)
  - [incrCharsets](#incrcharsets) (_This one uses 's' because plural_)
  - [currentDate](#currentdate)
  - [currentUnixTimestamp](#currentunixtimestamp)
- [Examples](#examples)

## JSON Schema

If you need _JSON Schema_ for this Draft, see [schema.json](/drafts/draft-1/schema.json) file.

## ISCI Formats

#### Root

```js
{
  "name": "string", // Optional
  "comment": "string", // Optional
  "pattern": "string", // Required
  "keywords": { keyword } // Required
}
```

- `name` - Free can be anything
- `comment` - You can fill in any comments that can make it easier for you or your team
- `pattern` - Use `<>` for parameter and `[]` for keyword. Ex: `<district_id>`, `[keywordName]`
- `keywords` - [keyword](#keyword)

#### `keyword`

```js
{
  "keywordName": keywordProperties
}
```

- `keywordName` - The name you use in `pattern`
- `keywordProperties` - [keywordProperties](#keywordproperties)

#### `keywordProperties`

```js
{
  "type": keywordTypes, // Required
  "comment": "string", // Optional
  ...etc // Different each type, depending on the keywordTypes
}
```

- `keywordTypes` - [Available Keyword Types](#available-keyword-types)
- `comment` - You can fill in any comments that can make it easier for you or your team

## Available Keyword Types

- [randCharset](#randcharset)
- [incrNumber](#incrnumber)
- [incrCharset](#incrcharset)
- [incrCharsets](#incrcharsets) (_This one uses 's' because plural_)
- [currentDate](#currentdate)
- [currentUnixTimestamp](#currentunixtimestamp)

### randCharset

Generate random strings from available charset.

#### Keyword Properties:

| Properties Name | Type            |
| --------------- | --------------- |
| type            | `"randCharset"` |
| length          | `number`        |
| minLength       | `number`        |
| maxLength       | `number`        |
| charset         | `string`        |

> You have to choose one, use `length` or use `minLength` and `maxLength`. The second choice causes the system to generate random length between `minLength` (_inclusive_) and `maxLength` (_inclusive_)

#### Example:

Options:

```json
{
  "type": "randCharset",
  "length": 6,
  "charset": "1234abcd"
}
```

Output: (Run 4x)

```bash
bdaa13
114a3b
b441c4
4dca4c
```

### incrNumber

Increment number with specific value.

#### Keyword Properties:

| Properties Name | Type           |
| --------------- | -------------- |
| type            | `"incrNumber"` |
| index           | `number`       |
| increaser       | `number`       |
| startNumber     | `number`       |

#### Example:

Options:

```json
{
  "type": "incrNumber",
  "index": 0,
  "increaser": 3,
  "startNumber": 1
}
```

Output: (Run 5x)

```bash
4
7
10
13
16
```

### incrCharset

Increment character based on its index position in charset.

#### Keyword Properties:

| Properties Name | Type            |
| --------------- | --------------- |
| type            | `"incrCharset"` |
| index           | `number`        |
| increaser       | `number`        |
| length          | `number`        |
| charset         | `string`        |

#### Example:

Options:

```json
{
  "type": "incrCharset",
  "index": 0,
  "increaser": 1,
  "length": 5,
  "charset": "abcdefg"
}
```

Output: (Run 6x)

```bash
aaaaa
aaaab
aaaac
aaaad
aaaae
aaaaf
```

### incrCharsets

Same as [`incrCharset`](#incrcharset), the difference is it uses many charsets at once and the length of result follow the length of the `charsets`.

#### Keyword Properties:

| Properties Name | Type             |
| --------------- | ---------------- |
| type            | `"incrCharsets"` |
| index           | `number`         |
| increaser       | `number`         |
| charsets        | `[string]`       |

#### Example:

Options:

```json
{
  "type": "incrCharsets",
  "index": 0,
  "increaser": 1,
  "charsets": ["abc", "123", "def", "ghi"]
}
```

Output: (Run 4x)

```bash
a1dg
a1dh
a1di
a1eg
```

### currentDate

Only date. nothing is different. it looks like no description is needed.

#### Keyword Properties:

| Properties Name | Type            |
| --------------- | --------------- |
| type            | `"currentDate"` |
| format          | `string`        |

> `format` string can be anything, but the following letters will be replaced (and leading zeroes added if necessary) ... See [date-format](https://github.com/nomiddlename/date-format#formatting-dates-as-strings) for more information.

#### Example:

Options:

```json
{
  "type": "currentDate",
  "format": "yyyy-MM-dd/hh-mm-ss.SSS"
}
```

Output: (Run 1x)

```bash
2020-01-09/15-00-00.000
```

### currentUnixTimestamp

Everything has been explained in [unixtimestamp.com](https://www.unixtimestamp.com/)

#### Keyword Properties:

| Properties Name | Type                     |
| --------------- | ------------------------ |
| type            | `"currentUnixTimestamp"` |

#### Example:

Options:

```json
{
  "type": "currentUnixTimestamp"
}
```

Output: (Run 3x)

```bash
1578560571114
1578560571116
1578560571117
```

## Examples

See [examples](/drafts/draft-1/examples) directory.

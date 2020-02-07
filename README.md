# ISCI - Identification Scheme Information

## List Contents

- [What is ISCI?](#what-is-isci)

- [Why should i use ISCI?](#why-should-i-use-isci)

- [Example](#example)

- [List ISCI Drafts](#list-isci-drafts)

  - [Draft-1](/drafts/draft-1)

- [Available ISCI Libraries](#available-isci-libraries)

- [FAQ](#faq)

## What is ISCI?

_ISCI_ (_Identification SCheme Information_) is a scheme that stores information related to an identification label. _ISCI_ can standardize an identification label on the system or application you have. _ISCI_ is very flexible. _ISCI_ uses the _JSON_ format, this format allows an identification label to generated on any system at any time. _ISCI_ can be stored in _Databases_, _JSON Files_ or other storage areas that support the _JSON_ storage format. _ISCI_ can be used across platforms depending on the availability of libraries on each platform.

## Why should i use ISCI?

ISCI allows you to create a flexible identification label. You can move ISCI wherever and whenever you want. ISCI will be very useful when the system you are using requires migration from one language to another. or in other cases such as moving physical servers from one place to another without disturbing identification labels that have been created and distributed before the move.

## Example

Example with ISCI [Draft-1](/drafts/draft-1):

The following is an ISCI which is used to create a _User ID_:

```json
{
  "name": "user-id",

  "pattern": "<district_id>-[unique_character]-[random_character]",

  "keywords": {
    "unique_character": {
      "type": "incrCharset",

      "length": 4,

      "index": 0,

      "increaser": 1,

      "charset": "abcdefghijklmnopqrstuvwxyz"
    },

    "random_character": {
      "type": "randCharset",

      "minLength": 3,

      "maxLength": 6,

      "charset": "abcdefgABCDEFGH0123456789",

      "comment": "Random characters make it difficult for people not to try to find IDs with dummy or bruteforce techniques"
    }
  }
}
```

> The `<district_id>` section will be entered by the user when creating the _ID_.

Results of ISCI above after being executed 5 times:

```bash

manager-aaaa-gDHgb3

employee-aaab-L4BA

employee-aaac-geFb

janitor-aaad-A9aB73

director-aaae-C7a5B

```

> See, the `district_id` section has changed automatically based on parameters passed at the time of _ID_ creation.

## List ISCI Drafts

- [Draft-1](/drafts/draft-1) - Release on **7 Feb 2020**

> Documentation is available in each draft. Visit the link provided to view the documentation of each draft.

## Available ISCI Libraries

- Javascript - [js-isci](https://github.com/laodemalfatih/js-isci)

> Have you write a new library? or have you write a new library with better performance? Please contact us to be included in the list.

## FAQ

### What format is used to create an ISCI?

ISCI uses the _JSON_ format.

### Where can i store an ISCI?

You can save it in a _JSON File_ or in a _Database_ that supports _JSON_ storage formats such as: _MongoDB_, _SQL_, _MYSQL_, _Solr_, _Redis_ (_as JSON String_) and etc.

### Is ISCI slow?

Absolutely not. Library [js-isci](https://github.com/laodemalfatih/js-isci) can generate up to _1,500,000_ _Unique ID_ (10 characters each) only in _1 Second_.

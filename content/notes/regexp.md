---
title: "Regular Expression"
date: 2020-08-28T00:53:22+05:30
draft: true
tags: []
categories: [misc]
sources:
  - https://github.com/ziishaned/learn-regex
---

<!--

::Annotation Guide::
~~~~~~~~~~~~~~~~~~~~

* `em` is the modifier

1. em (_text_) - blue underline
2. strong (**text**) - yelow highlight
3. del (~~text~~) - red strike-through

4. em > em (_*text*_) - blue circle
5. em > strong (_**text**_) - lawngreen box
6. em > del (_~~text~~_) - red cross-off
-->

A regular expression is a **group of characters or symbols** which is used
to find a **specific pattern in a text**.

![regex](https://raw.githubusercontent.com/ziishaned/learn-regex/master/img/regexp-en.png)

- a string literal is the simplest possible regular expression. `"str"` would
  match _**str(`s` followed by `t`, followed by `r`)**_.
- regular expression are generally **case sensitive**

## Meta Characters

- special characters. does not mean anything on their own.
- some meta character have different meaning when written inside square bracket

| meta char               | desc                                                                           |
| :---------------------- | :----------------------------------------------------------------------------- |
| `.`                     | match any single character except for linebreak                                |
| `[]`                    | char class. matches any char contained between the brackets                    |
| `[^ ]`                  | negated char class. matches any character _NOT_ contained between the brackets |
| `*`                     | matches 0 or more repetitions of the preceeding symbol                         |
| `+`                     | match one or more repetitions of preceeding symbol                             |
| `?`                     | makes the preceeding symbol optional                                           |
| `{n,m}`                 | match at least `n` but not more than `m` repetitions of preceeding symbol      |
| `(abc)`                 | char group                                                                     |
| `|`                     | alteration. matches either the chars before or the chars after the symbol      |
| `\` | escapes character |
| `^`                     | beginning of the input                                                         |
| `$`                     | end of the input                                                               |

- set **character range** by using **hyphen** inside character class.
Example: `/[a-z0-9]/`.

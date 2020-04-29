---
layout: page
title: Snippets
description: Collection of commonly used helpful, code snippets
---

#### Scale JPEG Images to 100 KB

Find JPEG images form a a directory and scale them up/down to 100 KB in size!

```sh
$ find . -maxdepth 1 -iname "*.jpg" | xargs -L1 -I{} convert -strip -define jpeg:extent=100kb -colorspace Gray -auto-level -monitor  "{}" out/"{}"
```

#### Change image src based on user's theme preference

This could be achived using HTML5 `picture` tag. [source](https://stackoverflow.com/a/56030447/8657006)

```html
<picture>
  <source srcset="night.jpg" media="(prefers-color-scheme: dark)" />
  <img src="day.jpg" />
</picture>
```

#### Hash a Password in Mongoose' pre-save hook using Node's Crypto module

`crypto` is a built-in Node.js module. This module could be used to hash and varify passwords pretty easily. Here's an implementation

```js
const MAX_ITERATIONS = 1000;
const KEY_LEN = 256;

userSchema.pre('save', function (next) {
  if (!this.isModified('password')) return next();

  this.salt = crypto.randomBytes(16);
  // generate hash and store it
  this.password = crypto
    .pbkdf2Sync(this.password, this.salt, MAX_ITERATIONS, KEY_LEN, 'sha512')
    .toString('hex');

  return next();
});
```

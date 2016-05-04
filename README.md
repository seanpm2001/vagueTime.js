# vagueTime.js

A tiny JavaScript library
that formats precise time differences
as a vague/fuzzy time.

[![Build status](https://secure.travis-ci.org/philbooth/vagueTime.js.png?branch=master)](http://travis-ci.org/#!/philbooth/vagueTime.js)

* [Why would I want that?](#why-would-i-want-that)
* [How tiny is it?](#how-tiny-is-it)
* [What doesn't it do?](#what-doesnt-it-do)
* [What alternative libraries are there?](#what-alternative-libraries-are-there)
* [How do I install it?](#how-do-i-install-it)
* [How do I use it?](#how-do-i-use-it)
  * [Loading the library](#loading-the-library)
  * [Calling the exported functions](#calling-the-exported-functions)
  * [Examples](#examples)
* [How do I set up the dev environment?](#how-do-i-set-up-the-dev-environment)
* [What changed between version 1.x and 2.x?](#what-changed-between-version-1x-and-2x)
* [What license is it released under?](#what-license-is-it-released-under)

## Why would I want that?

Displaying precise dates and times
can make a website feel stuffy and formal.
Using vague or fuzzy time phrases
like 'just now' or '3 days ago'
can contribute to a friendlier interface.

vagueTime.js provides a small, clean API
for translating timestamps
into user-friendly phrases,
heavily supported by unit tests.

## How tiny is it?

3.2 kb unminified with comments,
1.1 kb minified or
0.6 kb minified+gzipped.

## What doesn't it do?

Older versions of this library
used to include translations into languages
other than English.
That translation process
was both [imperfect](https://github.com/philbooth/vagueTime.js/issues/21)
and [a source of complexity](https://github.com/philbooth/vagueTime.js/issues/8),
whereas the raison d'être for this library
was to be small and simple.
Localisation is a separate problem,
best solved by a dedicated solution
so, in an effort to [do one thing well](https://en.wikipedia.org/wiki/Unix_philosophy),
I [removed the translation code]().
It is still available
in the [1.x branch](https://github.com/philbooth/vagueTime.js/tree/1.x) and,
of course,
you are welcome to fork this repo
if you preferred things
how they were.

This library also only converts
in one direction:
from dates/timestamps
to strings.
If you're interested
in the opposite transformation,
look elsewhere.

## What alternative libraries are there?

* [date.js](http://www.datejs.com/)
* [moment.js](http://momentjs.com/)
* [xdate](http://arshaw.com/xdate)
* [countdown.js](http://countdownjs.org/)

## How do I install it?

Via npm:

```
npm install vague-time
```

Or if you just want
the git repo:

```
git clone git@github.com:philbooth/vagueTime.js.git
```

## How do I use it?

### Loading the library

If you are running in
Node.js,
Browserify
or another CommonJS-style
environment,
you can `require`
vagueTime.js like so:

```javascript
var vagueTime = require('vague-time');
```

It also the supports
the AMD-style format
preferred by Require.js.

If you are
including vagueTime.js
with an HTML `<script>` tag,
or neither of the above environments
are detected,
the interface will be globally available
as `vagueTime`.

### Calling the exported functions

vagueTime.js exports a single public function, `get`,
which returns a vague time string
based on the argument(s) that you pass it.

The arguments are passed as properties
on a single options object:

* `from`:
  Timestamp or `Date` instance denoting the origin point from which the vague time will be calculated.
  Defaults to `Date.now()`.
* `to`:
  Timestamp or `Date` instance denoting the target point to which the vague time will be calculated.
  Defaults to `Date.now()`.
* `units`:
  String denoting the units that the `from` and `to` timestamps are specified in.
  May be `'s'` for seconds or `'ms'` for milliseconds.
  Defaults to `'ms'`.
  This property has no effect
  when `from` and `to` are `Date` instances
  rather than timestamps.

Essentially,
if `to` is less than `from`,
the returned vague time will indicate
some point in the past.
If `to` is greater than `from`,
it will indicate
some point in the future.

### Examples

```javascript
vagueTime.get({
  from: 60,
  to: 0,
  units: 's'
}); // returns 'a minute ago'

vagueTime.get({
  from: 0,
  to: 3600000,
  units: 'ms'
}); // returns 'in an hour'

vagueTime.get({
  from: new Date(2017, 0, 31),
  to: new Date(2016, 10, 30)
}); // returns '2 months ago'
```

## How do I set up the dev environment?

Install the dependencies:

```
npm i
```

Lint the code:

```
npm run lint
```

Run the tests:

```
npm test
```

Or, to run the tests in a web browser,
open `test/vagueTime.html`.

## What changed between version 1.x and 2.x?

Support for languages
other than English
was removed in release `2.0.0`.
If you were relying on that stuff,
I'm sorry.
You may be interested in
the [1.x branch](https://github.com/philbooth/vagueTime.js/tree/1.x).

## What license is it released under?

[MIT](COPYING)


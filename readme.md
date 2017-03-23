# key-cache

[sorry the code has something wrong](./README-CN.md)

Storing data in the form of key into the file

---

[![code style fecs](https://img.shields.io/badge/code%20style-fecs-brightgreen.svg)]()
[![NPM Version](https://img.shields.io/npm/v/key-cache.svg)]()
[![NPM Downloads](https://img.shields.io/npm/dm/key-cache.svg)]()
[![Linux Build](https://img.shields.io/travis/xuexb/key-cache/master.svg?label=linux)]()
[![Windows Build](https://img.shields.io/appveyor/ci/xuexb/key-cache/master.svg?label=windows)]()
[![Test Coverage](https://img.shields.io/coveralls/xuexb/key-cache/master.svg)]()
[![Dependencies](https://img.shields.io/david/xuexb/key-cache.svg?style=flat)]()
[![DevDependencies](https://img.shields.io/david/dev/xuexb/key-cache.svg?style=flat)]()

## Install

> requires node 0.12+

```bash
npm install key-cache --save
```

## Use

```js
// Create reference
var KeyCache = require('key-cache');

// Examples of objects
var cache = new KeyCache(options);

// Here you can use to manipulate the cache api
cache.get('balbalbal');
```

## The default configuration

### options.dir

Cache directory path based on the current run directory

```js
/**
 * @default key-cache installation path of .cache/ directory
 * @type {String}
 */
```

### options.timeout

Save time, in seconds, if empty will always exist

```js
/**
 * @default null
 * @type {number|null}
 */
```

### options.md5key

Set whether to use md5 named cache file name，To path is valid, it will filter the illegal character key, in addition to Chinese, letters, numbers, -, other characters will be ignored outside _, regular use is`/[^\u4e00-\u9fa5a-zA-Z\_\-0-9]/g`.

```js
/**
 * @default true
 * @type {Boolean}
 */
```

## Api

### set

Write data to a file

```js
/**
 * @param {string} key
 * @param {Object|string} value
 * @param {Object|undefined} options        If there will override the default configuration
 * @return {Object} this
 */
set(key, value, options = {})
```

### get

Get data from files

```js
/**
 * @param  {string} key
 *
 * @return {Object|string|null}             If there is no time has expired or will return null
 */
get(key)
```

### remove

Delete data, and delete files

```js
/**
 * @param  {string|undefined} key
 *
 * @return {Object}     this
 */
remove(key)
```

## Examples

### Simple

```js
var cache = new KeyCache();

cache.set('name', 'key-cache');

console.log(cache.get('name'));

cache.remove('name');

console.log(cache.get('name')); // => null
```

### Custom cache directory

```js
var cache = new KeyCache({
    dir: '../cache/'
});

cache.set('name', 'key-cache');

// override the default configuration
cache.set('name2', 'key-cache', {
    dir: './cache2'
});
```

### Set the expiration time

```js
var cache = new KeyCache({
    timeout: 3
});

cache.set('name', 'key-cache');

// override the default configuration
cache.set('age', 1, {
    timeout: 5
});

setTimeout(function(){
    console.log(cache.get('name')); // => null
    console.log(cache.get('age')); // => 1
}, 3000);
```

### Delete Cache

```js
var cache = new KeyCache();

cache.set('name', 'key-cache');
cache.set('age', 1);

// Delete single
cache.remove('name');

console.log(cache.get('name')); // => null
console.log(cache.get('age')); // => 1

// Delete all
cache.remove();

console.log(cache.get('age')); // => null
```

### md5key

> Do not use md5 named cache file

```js
var cache = new KeyCache({
    md5key: false
});

cache.set('key', 'key-cache'); // => filename is key.json
cache.set('age', 1); // => filename is age.json
cache.set('this a space +-', 1); // => filename is thisaspace-.json
cache.set('中文', 1); // => filename is 中文.json
```

## Develop

> Use es6 development, compiler-dependent [babel 6.x](https://babeljs.io/)

```js
// Run the compiler, the es6 code from the compiled into lib in src
npm run compile

// Monitor file changes and runs the compiler
npm run watch

// Use fecs run Style Checker
npm run check

// Use mocha run the test case
npm run test

// Run the test cases and code coverage
npm run test-cov
```

## Changelog

### 0.2.0

Add `options.md5key` parameter is used to set whether to use md5 named cache file name

### 0.1.x

Optimized code, add a test case

## License

MIT

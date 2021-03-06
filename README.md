# Qute

A better async queue using promises.

[![Build Status](https://travis-ci.org/Moeriki/node-qute.svg?branch=master)](https://travis-ci.org/Moeriki/node-qute) [![Coverage Status](https://coveralls.io/repos/github/Moeriki/node-qute/badge.svg?branch=master)](https://coveralls.io/github/Moeriki/node-qute?branch=master) [![Known Vulnerabilities](https://snyk.io/test/github/moeriki/node-qute/badge.svg)](https://snyk.io/test/github/moeriki/node-qute) [![dependencies Status](https://david-dm.org/moeriki/node-qute/status.svg)](https://david-dm.org/moeriki/node-qute) [![Downloads](http://img.shields.io/npm/dm/qute.svg?style=flat)](https://www.npmjs.org/package/qute)

## Install

```sh
npm install --save qute
```

## Usage

```javascript
const qute = require('qute');
const queue = qute({ maxConcurrency: 1 });

queue.push(
  () => new Promise((resolve) => {
    setTimeout(() => resolve('OK 1'), 1000);
  },
  () => new Promise((resolve) => {
    setTimeout(() => resolve('OK 2'), 1000);
  }
).then((result) => {
  // result = ['OK 1', 'OK 2']
});

queue.size(); // 2
queue.sizePending(); // 1
queue.sizeQueued(); // 1

```

## API

**qute( options:object )** create a queue

* *options.maxConcurrency* tasks to run simeltaneously (default: 1)
* *option.paused* start queue paused (default: false)

**queue.push( ...tasks:function )**

append tasks to the queue

**queue.unshift( ...tasks:function )**

prepend tasks to the queue

**queue.pause()** / **queue.resume()**

pause / resume starting new tasks

**queue.size()** count of unfinished tasks

**queue.sizePending()** count of running tasks

**queue.sizeQueued()** count of tasks not running

## any-promise

Qute uses [any promise](https://github.com/kevinbeaty/any-promise) to detect a Promise object. Check [their README](https://github.com/kevinbeaty/any-promise#any-promise) to plugin in your own Promise library.

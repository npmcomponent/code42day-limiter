*This repository is a mirror of the [component](http://component.io) module [code42day/limiter](http://github.com/code42day/limiter). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/code42day-limiter`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*
[![Build Status](https://img.shields.io/travis/code42day/limiter.svg)](http://travis-ci.org/code42day/limiter)

# limiter

  Limits the rate of function calls to one per period. It delays but does not throttle the calls.
  Useful when your codes needs to behave well when calling rate limited API.

  If you need something more flexible use [rate limiter](https://npmjs.org/package/limiter)

## Installation

    $ component install code42day/limiter


## Usage

Create `limiter` with desired `interval` setting. Call `trigger` passing a function that you want to
limit.

```javascript
var limiter = require('limiter'),
	l = limiter(500); // interval in millis

function doThis() {
  // this is called at most twice per second
}

function doThat() {
  // you can rate limit different functions
}


l.trigger(doThis);
l.trigger(doThat);
l.trigger(doThis);
l.trigger(function() {
	l.penalty(); // wait a bit longer next time
});
l.trigger(doThat);
```

## API

### limiter(interval, [penaltyInterval])

Create `limiter` with desired `interval` (in millis). Optional `penaltyInterval` is used instead of
`interval` if `limiter.penalty()` has been called at least once since last limited function has been
triggered.

### trigger(fn)

Add `fn` to `limiter` queue. It will be called when `interval` elapsed since another function from
the queue was called.

### penalty()

Make limiter to use `penaltyInterval` before triggering next function.

### cancel()

Empty `limiter` queue. Remove all pending trigger request. No methods from the queue is called after
`cancel`.

## License

  MIT

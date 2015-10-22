Parse
===
[![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Coverage Status][codecov-image]][codecov-url] [![Dependencies][dependencies-image]][dependencies-url]

> Attempts to parse an input string as [commented JSON](https://github.com/kof/node-cjson).


## Installation

``` bash
$ npm install utils-cjson-parse
```


## Usage

``` javascript
var parse = require( 'utils-cjson-parse' );
```

#### parse( value[, reviver] )

Attempts to parse an input `string` as [commented JSON](https://github.com/kof/node-cjson).

``` javascript
var out = parse( '{"beep":"boop"}' );
// returns {'beep':'boop'}

out = parse( '{beep:boop"}' );
// returns <SyntaxError>
```

The API is the same as [`cjson#parse`](https://github.com/kof/node-cjson). Hence, to use a custom `reviver` function

``` javascript
var out;

function reviver( key, value ) {
	if ( key === '' ) {
		return value;
	}
	if ( key === 'beep' ) {
		return value;
	}
}

out = parse( '{"beep":"boop","a":"b"}', reviver );
// returns {'beep':'boop'}
```


## Notes

*	This `function` wraps [`cjson#parse`](https://github.com/kof/node-cjson) in a `try/catch` block.
*	The presence of `try/catch` within any `function` prevents JavaScript compiler optimization. By isolating the `try/catch` block, we minimize the extent of optimization hell.


## Examples

``` javascript
var fs = require( 'fs' ),
	path = require( 'path' ),
	parse = require( 'utils-cjson-parse' );

// Load a commented JSON file...
var file = path.resolve( '/path/to/file.cjson' );
file = fs.readFileSync( file, {
	'encoding': 'utf8'
});

// Attempt to parse the file...
file = parse( file );
console.dir( file );
```

To run the example code from the top-level application directory,

``` bash
$ node ./examples/index.js
```


## Tests

### Unit

Unit tests use the [Mocha](http://mochajs.org/) test framework with [Chai](http://chaijs.com) assertions. To run the tests, execute the following command in the top-level application directory:

``` bash
$ make test
```

All new feature development should have corresponding unit tests to validate correct functionality.


### Test Coverage

This repository uses [Istanbul](https://github.com/gotwarlost/istanbul) as its code coverage tool. To generate a test coverage report, execute the following command in the top-level application directory:

``` bash
$ make test-cov
```

Istanbul creates a `./reports/coverage` directory. To access an HTML version of the report,

``` bash
$ make view-cov
```


---
## License

[MIT license](http://opensource.org/licenses/MIT).


## Copyright

Copyright &copy; 2015. Athan Reines.


[npm-image]: http://img.shields.io/npm/v/utils-cjson-parse.svg
[npm-url]: https://npmjs.org/package/utils-cjson-parse

[travis-image]: http://img.shields.io/travis/kgryte/utils-cjson-parse/master.svg
[travis-url]: https://travis-ci.org/kgryte/utils-cjson-parse

[codecov-image]: https://img.shields.io/codecov/c/github/kgryte/utils-cjson-parse/master.svg
[codecov-url]: https://codecov.io/github/kgryte/utils-cjson-parse?branch=master

[dependencies-image]: http://img.shields.io/david/kgryte/utils-cjson-parse.svg
[dependencies-url]: https://david-dm.org/kgryte/utils-cjson-parse

[dev-dependencies-image]: http://img.shields.io/david/dev/kgryte/utils-cjson-parse.svg
[dev-dependencies-url]: https://david-dm.org/dev/kgryte/utils-cjson-parse

[github-issues-image]: http://img.shields.io/github/issues/kgryte/utils-cjson-parse.svg
[github-issues-url]: https://github.com/kgryte/utils-cjson-parse/issues

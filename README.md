<!--

@license Apache-2.0

Copyright (c) 2021 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->

# Add-on Arguments

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> C API for validating, extracting, and transforming (to native C types) function arguments provided to an ndarray Node-API add-on interface.

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- Package usage documentation. -->

<section class="installation">

## Installation

```bash
npm install @stdlib/ndarray-base-napi-addon-arguments
```

</section>

<section class="usage">

## Usage

```javascript
var headerDir = require( '@stdlib/ndarray-base-napi-addon-arguments' );
```

#### headerDir

Absolute file path for the directory containing header files for C APIs.

```javascript
var dir = headerDir;
// returns <string>
```

</section>

<!-- /.usage -->

<!-- Package usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- Package usage examples. -->

<section class="examples">

## Examples

```javascript
var headerDir = require( '@stdlib/ndarray-base-napi-addon-arguments' );

console.log( headerDir );
// => <string>
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->

* * *

<section class="c">

## C APIs

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- C usage documentation. -->

<section class="usage">

### Usage

```c
#include "stdlib/ndarray/base/napi/addon_arguments.h"
```

<!-- lint disable maximum-heading-length -->

#### stdlib_ndarray_napi_addon_arguments( env, argv, nargs, nin, \*arrays\[], \*err )

Validates, extracts, and transforms (to native C types) function arguments provided to an ndarray Node-API add-on interface.

```c
#include <node_api.h>
#include <stdint.h>
#include <assert.h>

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    napi_status status;

    // ...

    int64_t nargs = 6;
    int64_t nin = 2;

    // Get callback arguments:
    size_t argc = 6;
    napi_value argv[ 6 ];
    status = napi_get_cb_info( env, info, &argc, argv, nullptr, nullptr );
    assert( status == napi_ok );

    // ...

    // Process the provided arguments:
    struct ndarray *arrays[ 3 ];

    napi_value err;
    status = stdlib_ndarray_napi_addon_arguments( env, argv, nargs, nin, arrays, &err );
    assert( status == napi_ok );

    // ...

}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **argv**: `[in] napi_value*` ndarray function arguments.
-   **nargs**: `[in] int64_t` total number of expected arguments.
-   **nin**: `[in] int64_t` number of input ndarray arguments.
-   **arrays**: `[out] struct ndarrays**` destination array for storing pointers to both input and output ndarrays.
-   **err**: `[out] napi_value*` pointer for storing a JavaScript error.

```c
napi_status stdlib_ndarray_napi_addon_arguments( const napi_env env, const napi_value *argv, const int64_t nargs, const int64_t nin, struct ndarray *arrays[], napi_value *err );
```

The function returns a `napi_status` status code indicating success or failure (returns `napi_ok` if success).

</section>

<!-- /.usage -->

<!-- C API usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

### Notes

-   The function assumes the following argument order:

    ```text
    [ ib1, im1, ib2, im2, ..., ob1, om1, ob2, om2, ... ]
    ```

    where

    -   `ib#` is a data buffer for an input ndarray.
    -   `im#` is meta data for an input ndarray.
    -   `ob#` is a data buffer for an output ndarray.
    -   `om#` is meta data for an output ndarray.

-   The function may return one of the following JavaScript errors:

    -   `Error`: unable to allocate memory when processing input ndarray.
    -   `Error`: unable to allocate memory when processing output ndarray.

</section>

<!-- /.notes -->

<!-- C API usage examples. -->

<section class="examples">

</section>

<!-- /.examples -->

</section>

<!-- /.c -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2022. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/ndarray-base-napi-addon-arguments.svg
[npm-url]: https://npmjs.org/package/@stdlib/ndarray-base-napi-addon-arguments

[test-image]: https://github.com/stdlib-js/ndarray-base-napi-addon-arguments/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/ndarray-base-napi-addon-arguments/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/ndarray-base-napi-addon-arguments/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/ndarray-base-napi-addon-arguments?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/ndarray-base-napi-addon-arguments.svg
[dependencies-url]: https://david-dm.org/stdlib-js/ndarray-base-napi-addon-arguments/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://gitter.im/stdlib-js/stdlib/

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/ndarray-base-napi-addon-arguments/main/LICENSE

</section>

<!-- /.links -->

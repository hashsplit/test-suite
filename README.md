This repository contains a conformance test suite for the [hashsplit][1]
specification.

Each subdirectory of the `tests` directory contains three files:

- a `README` describing the significance of the tests in that directory,
- one test input in a file called `input`,
- and configuration in a file `configs.json`.

The structure of the latter is a json object of the form:

```json
{
  "cases": {
    "test-1": {
      "config": {
        "minSize": 32768,
        "maxSize": 1048576,
        "hash": "rrs1",
        "threshold": 13
      },
      "sizes": [40000, 33350, 100000]
    },
    "test-2": {
      "config": {
        "minSize": 1024,
        "maxSize": 65536,
        "hash": "rrs1",
        "threshold": 12
      },
      "sizes": [1342, 8241, 64231, 32121, 37415]
    }
  }
}
```

Where each item in `"cases"` contains one test case using the input
file. The `"config"` field contains the configuration that should
be used when splitting, and the `"sizes"` field is a list containing the
size of each chunk in the input, in bytes, for the given config.

Implementations should use this test data to confirm that on each input
and config, the implementation creates chunks of the correct sizes.

Implementations should also test other properties, such as:

- For all inputs,the concatenation of the chunks is equal to the input.
- TODO: add other suggestions

The format will probably be tweaked later to support testing the tree
construction algorithm.

[1]: https://github.com/hashsplit/hashsplit-spec
[2]: https://github.com/hashsplit/hashsplit-spec/issues/21

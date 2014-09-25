Contributing
============

A guide to contributing to [doc-metrix](https://github.com/doc-metrix/overview): documentation and utilities for computer metrics.


## Table of Contents

1. 	[Naming Conventions](#naming-conventions)
1. 	[Documentation](#documentation)
	* 	[Versioning](#versioning)
1. 	[Utilities](#utilities)
	* 	[Docs](#docs)
	* 	[Examples](#examples)
	* 	[Style Guides](#style-guides)
	* 	[Tests](#tests)
		- 	[Unit](#unit)
		- 	[Coverage](#coverage)
1. 	[License](#license)


===
### Naming Conventions

Documentation repository names should describe the metrics included in the documentation. For example, documentation describing CPU related metrics should be named `cpu`. Documentation describing memory related metrics should be named `memory` or shortened to `mem`. Additional examples include `network`, `sensors-power`, `sensors-temperature`, `processes`, `vm`, etc.

Metric names should use dot notation. For example,

``` javascript
// Do:
cpu.utilization

// Don't:
cpu-utilization
cpu utilization
cpu_utilization
cpu:utilization
cpu~utilization
```

For complex metric names, use camel-casing.

``` javascript
// Do:
mem.memFree

// Don't:
mem.memfree
mem.Memfree
mem.MemFree
```

Utility module names should indicate the language and, where applicable, the particular metric documentation used. For example, a Node.js module which provides access to cpu metric documentation should be named `cpu-node`. Similarly, a Go module providing similar access should be named `cpu-go`.


===
### Documentation

Metric documentation describes a particular subset of computer performance metrics. Documentation should be a JSON file listing detailed metric information. For example, consider the documentation for `cpu.user`:

``` javascript
{

    "displayName": "User Mode Percentage",
    "units": "percent",
    "max": 1,
    "min": 0,
    "sigFigs": null,
    "dataType": "percentage",
    "type": "derived",
    "formula": {
      "equation": "\\frac{t_{user}}{t_{up}}",
      "variables": {
        "t_{user}": {
          "description": "the amount of time spent processing user tasks"
        },
        "t_{up}": {
          "description": "the amount of time since last reboot"
        }
      }
    },
    "description": "Percentage of time spent executing processes in user mode.",
    "notes": "Time is measured in units of USER_HZ, which is 1/100th of a second (a jiffy) on most architectures.",
    "device": "^cpu\\d+$",
    "classification": "cpu",
    "refs": [
      "http://linux.die.net/man/5/proc"
    ]
}
```

The documentation includes:

-	  display name
- 	description
- 	units
-	  significant figures (if calculated)
- 	minimum value
- 	maximum value
- 	data type (count, percentage, time, etc)
-	  metric type (raw or derived)
- 	formula, including variable descriptions
-	  notes
- 	metric classification
-	  reporting devices
- 	references for additional information

For additional information, see the JSON [schema](https://github.com/doc-metrix/schema) and see the [documentation generator](https://github.com/doc-metrix/generator-doc-metrix-doc) which creates a scaffold to expedite documentation writing.



===
#### Versioning

All documentation should have versions. Documentation should be initialized with version `0.0.0`. Any updates to the documentation should be tagged.

``` bash
$ git tag -a <major.minor.patch> -m "Version."
$ git push origin <major.minor.patch>
```

Use [semantic versioning](http://semver.org/) (semvar) for communicating versions.

*	Any new metrics should be communicated as `minor` updates.
*	Any corrections/value modifications should be `patches`.
* Any documentation restructuring (changing field names, removing fields, etc) should be communicated as a `major` update.


===
### Utilities

Utilities provide means to parse and implement documentation. For example, a module which handles a `mem.Free` data stream may need to perform unit conversion. By importing memory documentation and extracting the metric units, the module can select the appropriate conversion formula for data transformation.


#### Docs

A utility module should include detailed documentation, typically provided in a `README.md`. The `README` should include a module description, example code, and license information.


#### Examples

A utility module should include executable example code demonstrating utility use.


#### Style Guides

Modules should adhere to the following style guides:

- 	[JavaScript](https://github.com/kgryte/javascript-style-guide)


#### Tests

##### Unit

All utility modules must include unit tests.


##### Coverage

Modules should strive for 100% test coverage.


---
## License

[MIT license](http://opensource.org/licenses/MIT). 


---
## Copyright

Copyright &copy; 2014. [NodePrime](http://nodeprime.com).


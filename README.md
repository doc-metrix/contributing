Contributing
============

A guide to contributing to [doc-metrix](https://github.com/doc-metrix/overview): documentation and utilities for computer metrics.


## Table of Contents

1. 	[Naming Conventions](#naming-conventions)
1. 	[Specifications](#specifications)
	* 	[Versioning](#versioning)
1. 	[Utilities](#utilities)
	* 	[Documentation](#documentation)
	* 	[Examples](#examples)
	* 	[Style Guides](#style-guides)
	* 	[Tests](#tests)
		- 	[Unit](#unit)
		- 	[Coverage](#coverage)
1. 	[License](#license)


===
### Naming Conventions

Specification repository names should describe the metrics included in the specification. For example, a specification describing CPU related metrics should be named `cpu`. A specification describing memory related metrics should be named `memory` or shortened to `mem`. Additional examples include `network`, `sensors-power`, `sensors-temperature`, `processes`, `vm`, etc.

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

Utility module names should indicate the language and, where applicable, the particular metric specification used. For example, a Node.js module which provides access to a cpu metric specification should be named `cpu-node`. Similarly, a Go module providing similar access should be named `cpu-go`.


===
### Specifications

Specifications are documents describing a particular subset of computer performance metrics. Specifications should be JSON documents listing detailed metric information. For example, consider the specification for `cpu.user`:

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
    "platforms": {
      "linux": ["/proc/stat", "/proc/cpuinfo"]
    },
    "device": "^cpu\\d+$",
    "vendors": "*",
    "classification": "cpu",
    "refs": [
      "http://linux.die.net/man/5/proc"
    ]
}
```

The specification includes:

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
- 	vendor support
-	  reporting devices
- 	references for additional information

For additional information, see the JSON [schema](https://github.com/doc-metrix/schema) and see the [specification generator](https://github.com/doc-metrix/generator-doc-metrix-spec) which creates a scaffold to expedite specification writing.



===
#### Versioning

All specifications should have versions. A specification should be initialized with version `0.0.0`. Any updates to the specification should be tagged.

``` bash
$ git tag -a <major.minor.patch> -m "Version."
$ git push origin <major.minor.patch>
```

Use [semantic versioning](http://semver.org/) (semvar) for communicating versions.

*	Any new metrics should be communicated as `minor` updates.
*	Any corrections/value modifications should be `patches`.
* 	Any specification restructuring (changing field names, removing fields, etc) should be communicated as a `major` update.


===
### Utilities

Utilities provide means to parse and implement specifications. For example, a module which handles a `mem.Free` data stream may need to perform unit conversion. By importing a memory specification and extracting the metric units, the module can select the appropriate conversion formula for data transformation.


#### Documentation

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


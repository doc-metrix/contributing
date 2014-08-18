Contributing
============

_doc-metrix_ provides documentation and utilities for computer metrics. To contribute to _doc-metrix_, please follow the guide provided below.


## Guide

### Naming Conventions

Specification repository names should describe the metrics included in the specification. For example, a specification describing CPU related metrics should be named `cpu`. A specification describing memory related metrics should be named `memory` or shortened to `mem`. Additional example include `network`, `sensors-power`, `sensors-temperature`, `processes`, `vm`, etc.

Utility module names should indicate the language and, where applicable, the particular metric specification used. For example, a Node.js module which provides access to a cpu metric specification would be named `cpu-node`. Similarly, a Go module providing similar access would be named `cpu-go`.


### Specifications

Specifications should be JSON documents listing detailed metric information. For example, consider the specification for `cpu.user`:

``` javascript
{}
```

The specification includes:

- 	metric name
-	display name
- 	description
- 	units
- 	min
- 	max
- 	formula
- 	source
- 	device
-	notes
- 	references




### Utilities

Utilities provide means to parse and implement specifications. For example, a module which handles a `mem.Free` data stream may need to perform unit conversion. By importing and caching the metric units, the module can select the appropriate conversion formula for data transformation.


#### Documentation

A utility module should include detailed documentation, typically provided in a `README.md`. The `README` should include a module description, example code, and license information.


#### Examples

A utility module should include executable example code demonstrating utility use.


#### Style

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


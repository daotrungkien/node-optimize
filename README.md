node-optimize-es
================

This is a modified version of `node-optimize` at https://github.com/danielgindi/node-optimize for compatibility with ECMAScript 6+. The original project was not updated for years.

[![npm Version](https://badge.fury.io/js/node-optimize-es.png)](https://npmjs.org/package/node-optimize-es)

We all need a tool to optimize a node.js project and create a single `js` file from it, 
Taking care of `require`s and leaving out `node_modules`.

Well I needed one too, and there wasn't one, so I build it!

Usage:
```javascript

	var NodeOptimizer = require('node-optimize');
	var optimizer = new NodeOptimizer({ 
		ignore: [
			'config/db.js',
			'private/some-other-file.js',
		]
	});
	
    var mergedJs = optimizer.merge('main.js'); // node-optimize will automatically resolve that path for 'main.js' using path.resolve(...)
	
	require('fs').writeFile(require('path').resolve('main.optimized.js'), mergedJs);
	
```

## What's in the bag

* `options.ignore` -> Tell it which files to ignore in the process of expanding the `require` calls.
* Automatically ignores core modules, or modules from `node_modules`.
* Currently handles `*.js`, `*.json`, and directory modules (with or without package.json/main).
* Functionality of `require` statements stay the same - loading on demand, loading once, and synthesizing the `module` global object.
* Handling of cyclic references same as node.js's' native implementation
* Using `include` option to include files which are not automatically detected (because of dynamic `require`s using variables and other complex loading mechanisms)
* Loading modules which were specified using complex `require` statement (i.e. `require(moduleName + '_' + index)`)

*Note*: Support for `require` of module folders (with parsing of `package.json` etc.) will be added in the future.

## License

All the code here is under MIT license. Which means you could do virtually anything with the code.
I will appreciate it very much if you keep an attribution where appropriate.

    The MIT License (MIT)

    Copyright (c) 2013 Daniel Cohen Gindi (danielgindi@gmail.com)

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.

# api documentation for  [event-emitter (v0.3.5)](https://github.com/medikoo/event-emitter#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-event-emitter.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-event-emitter) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-event-emitter.svg)](https://travis-ci.org/npmdoc/node-npmdoc-event-emitter)
#### Environment agnostic event emitter

[![NPM](https://nodei.co/npm/event-emitter.png?downloads=true)](https://www.npmjs.com/package/event-emitter)

[![apidoc](https://npmdoc.github.io/node-npmdoc-event-emitter/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-event-emitter_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-event-emitter/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-event-emitter/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-event-emitter/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Mariusz Nowak",
        "email": "medyk@medikoo.com",
        "url": "http://www.medikoo.com/"
    },
    "bugs": {
        "url": "https://github.com/medikoo/event-emitter/issues"
    },
    "dependencies": {
        "d": "1",
        "es5-ext": "~0.10.14"
    },
    "description": "Environment agnostic event emitter",
    "devDependencies": {
        "tad": "~0.2.7",
        "xlint": "~0.2.2",
        "xlint-jslint-medikoo": "~0.1.4"
    },
    "directories": {},
    "dist": {
        "shasum": "df8c69eef1647923c7157b9ce83840610b02cc39",
        "tarball": "https://registry.npmjs.org/event-emitter/-/event-emitter-0.3.5.tgz"
    },
    "gitHead": "b951397b8f0d55fc7ae8aea7fa7699e48132a53d",
    "homepage": "https://github.com/medikoo/event-emitter#readme",
    "keywords": [
        "event",
        "events",
        "trigger",
        "observer",
        "listener",
        "emitter",
        "pubsub"
    ],
    "license": "MIT",
    "maintainers": [
        {
            "name": "medikoo",
            "email": "medikoo+npm@medikoo.com"
        }
    ],
    "name": "event-emitter",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/medikoo/event-emitter.git"
    },
    "scripts": {
        "lint": "node node_modules/xlint/bin/xlint --linter=node_modules/xlint-jslint-medikoo/index.js --no-cache --no-stream",
        "lint-console": "node node_modules/xlint/bin/xlint --linter=node_modules/xlint-jslint-medikoo/index.js --watch",
        "test": "node ./node_modules/tad/bin/tad"
    },
    "version": "0.3.5"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module event-emitter](#apidoc.module.event-emitter)
1.  object <span class="apidocSignatureSpan">event-emitter.</span>methods

#### [module event-emitter.methods](#apidoc.module.event-emitter.methods)
1.  [function <span class="apidocSignatureSpan">event-emitter.methods.</span>emit (type)](#apidoc.element.event-emitter.methods.emit)
1.  [function <span class="apidocSignatureSpan">event-emitter.methods.</span>off (type, listener)](#apidoc.element.event-emitter.methods.off)
1.  [function <span class="apidocSignatureSpan">event-emitter.methods.</span>on (type, listener)](#apidoc.element.event-emitter.methods.on)
1.  [function <span class="apidocSignatureSpan">event-emitter.methods.</span>once (type, listener)](#apidoc.element.event-emitter.methods.once)



# <a name="apidoc.module.event-emitter"></a>[module event-emitter](#apidoc.module.event-emitter)



# <a name="apidoc.module.event-emitter.methods"></a>[module event-emitter.methods](#apidoc.module.event-emitter.methods)

#### <a name="apidoc.element.event-emitter.methods.emit"></a>[function <span class="apidocSignatureSpan">event-emitter.methods.</span>emit (type)](#apidoc.element.event-emitter.methods.emit)
- description and source-code
```javascript
emit = function (type) {
	var i, l, listener, listeners, args;

	if (!hasOwnProperty.call(this, '__ee__')) return;
	listeners = this.__ee__[type];
	if (!listeners) return;

	if (typeof listeners === 'object') {
		l = arguments.length;
		args = new Array(l - 1);
		for (i = 1; i < l; ++i) args[i - 1] = arguments[i];

		listeners = listeners.slice();
		for (i = 0; (listener = listeners[i]); ++i) {
			apply.call(listener, this, args);
		}
	} else {
		switch (arguments.length) {
		case 1:
			call.call(listeners, this);
			break;
		case 2:
			call.call(listeners, this, arguments[1]);
			break;
		case 3:
			call.call(listeners, this, arguments[1], arguments[2]);
			break;
		default:
			l = arguments.length;
			args = new Array(l - 1);
			for (i = 1; i < l; ++i) {
				args[i - 1] = arguments[i];
			}
			apply.call(listeners, this, args);
		}
	}
}
```
- example usage
```shell
...
  // … react to 'test' event
});

emitter.once('test', function (args) {
  // … react to first 'test' event (invoked only once!)
});

emitter.emit('test', arg1, arg2/*…args*/); // Two above listeners invoked
emitter.emit('test', arg1, arg2/*…args*/); // Only first listener invoked

emitter.off('test', listener);              // Removed first listener
emitter.emit('test', arg1, arg2/*…args*/); // No listeners invoked
'''
### Additional utilities
...
```

#### <a name="apidoc.element.event-emitter.methods.off"></a>[function <span class="apidocSignatureSpan">event-emitter.methods.</span>off (type, listener)](#apidoc.element.event-emitter.methods.off)
- description and source-code
```javascript
off = function (type, listener) {
	var data, listeners, candidate, i;

	callable(listener);

	if (!hasOwnProperty.call(this, '__ee__')) return this;
	data = this.__ee__;
	if (!data[type]) return this;
	listeners = data[type];

	if (typeof listeners === 'object') {
		for (i = 0; (candidate = listeners[i]); ++i) {
			if ((candidate === listener) ||
					(candidate.__eeOnceListener__ === listener)) {
				if (listeners.length === 2) data[type] = listeners[i ? 0 : 1];
				else listeners.splice(i, 1);
			}
		}
	} else {
		if ((listeners === listener) ||
				(listeners.__eeOnceListener__ === listener)) {
			delete data[type];
		}
	}

	return this;
}
```
- example usage
```shell
...
emitter.once('test', function (args) {
  // … react to first 'test' event (invoked only once!)
});

emitter.emit('test', arg1, arg2/*…args*/); // Two above listeners invoked
emitter.emit('test', arg1, arg2/*…args*/); // Only first listener invoked

emitter.off('test', listener);              // Removed first listener
emitter.emit('test', arg1, arg2/*…args*/); // No listeners invoked
'''
### Additional utilities

#### allOff(obj) _(event-emitter/all-off)_

Removes all listeners from given event emitter object
...
```

#### <a name="apidoc.element.event-emitter.methods.on"></a>[function <span class="apidocSignatureSpan">event-emitter.methods.</span>on (type, listener)](#apidoc.element.event-emitter.methods.on)
- description and source-code
```javascript
on = function (type, listener) {
	var data;

	callable(listener);

	if (!hasOwnProperty.call(this, '__ee__')) {
		data = descriptor.value = create(null);
		defineProperty(this, '__ee__', descriptor);
		descriptor.value = null;
	} else {
		data = this.__ee__;
	}
	if (!data[type]) data[type] = listener;
	else if (typeof data[type] === 'object') data[type].push(listener);
	else data[type] = [data[type], listener];

	return this;
}
```
- example usage
```shell
...
var ee = require('event-emitter');

var MyClass = function () { /* .. */ };
ee(MyClass.prototype); // All instances of MyClass will expose event-emitter interface

var emitter = new MyClass(), listener;

emitter.on('test', listener = function (args) {
  // … react to 'test' event
});

emitter.once('test', function (args) {
  // … react to first 'test' event (invoked only once!)
});
...
```

#### <a name="apidoc.element.event-emitter.methods.once"></a>[function <span class="apidocSignatureSpan">event-emitter.methods.</span>once (type, listener)](#apidoc.element.event-emitter.methods.once)
- description and source-code
```javascript
once = function (type, listener) {
	var once, self;

	callable(listener);
	self = this;
	on.call(this, type, once = function () {
		off.call(self, type, once);
		apply.call(listener, this, arguments);
	});

	once.__eeOnceListener__ = listener;
	return this;
}
```
- example usage
```shell
...

var emitter = new MyClass(), listener;

emitter.on('test', listener = function (args) {
  // … react to 'test' event
});

emitter.once('test', function (args) {
  // … react to first 'test' event (invoked only once!)
});

emitter.emit('test', arg1, arg2/*…args*/); // Two above listeners invoked
emitter.emit('test', arg1, arg2/*…args*/); // Only first listener invoked

emitter.off('test', listener);              // Removed first listener
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)

# esdoc-babel-plugin

Modified to work with *babel 7's* latest.

This plugin will run code through a certain set of babel plugins before giving it back to esdoc.
This can be used, for example, to remove certain syntax not supported by esdoc.

## Install and usage

```sh
npm install --save-dev mhelvens/esdoc-babel-plugin
```

Make sure you also install `babel-core` (version 6 or higher) and
the babel plugins you want to use. For example:

```sh
npm install --save-dev babel-core babel-plugin-angular2-annotations babel-plugin-transform-decorators-legacy babel-plugin-transform-flow-strip-types
```

Configure esdoc to use this plugin, and specify the set of babel plugins you wish to run,
in `.esdoc.json`:

```javascript
{
  "source": "./src",
  "destination": "./dist/docs",
  "plugins": [


		{"name": "esdoc-ecmascript-proposal-plugin", "option": {"all": true}},
			{"name": "esdoc-standard-plugin"},

		{
      "name": "esdoc-babel-plugin",
      "option": {
        "plugins": [
					[
						"@babel/plugin-transform-runtime",
						{
							"absoluteRuntime": true,
							"corejs": false,
							"helpers": true,
							"regenerator": true,
							"useESModules": true
						}
					],

					["@babel/plugin-proposal-decorators", {
						"legacy": true
					}],
					"@babel/plugin-proposal-function-sent",
					"@babel/plugin-proposal-export-namespace-from",
					"@babel/plugin-proposal-export-default-from",
					"@babel/plugin-proposal-numeric-separator",
					"@babel/plugin-proposal-throw-expressions",
					"@babel/plugin-syntax-dynamic-import",
					"@babel/plugin-syntax-import-meta",
					"@babel/plugin-syntax-flow",
					[
						"@babel/plugin-proposal-class-properties", {
							"ignoreUninitialized":	true
						}
					],
					["@babel/plugin-proposal-json-strings"],
					["@babel/plugin-transform-flow-strip-types"]
				]
      }
    }
	]
}

```

Note that the `"option"` object is passed directly to babel, so it supports all options
that babel supports.

Execute ESDoc:

```sh
esdoc
```

## License

MIT

## Authors

Maintained by [Ryan Spice](https://ryanspice.com/)

Originally based on `esdoc-babel-plugin` by [Michiel Helvensteijn](http://www.mhelvens.net).

Originally based on `esdoc-flow-plugin` by [Edgardo Avilés @eaviles](https://twitter.com/eaviles).

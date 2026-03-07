# NPM

Using NPM dependencies consists of basically using `NPM` meta-data over variables and interoperating with these variables using built-in packages like `org.js.g.*`, `org.node.g.*`, `org.node.fs.*` and `org.w3.web.*`.

Note that `NPM` annotatated variables are always `org.js.g.Object` instances that wrap an underlying JavaScript value; it's not entirely reliable to use the `is`, `as`, `T(v)` and `===` operators with them. You may explore these wrapper APIs for more ideas.

```sx
[NPM(importDefault="foo")]
var foo;
[NPM(importAll="foo")]
var foo;

foo.x // org.js.g.Object
```

## Browser and NodeJS distinguishment

Whack Red internally uses RollupJS as a JS bundler + the node-resolve plugin.

- Whack Red intercepts module resolution (through a mini plugin) so that for web builds, `node:` prefixed modules and most of the implicit NodeJS modules (such as `path` and `fs`, that do not exist in `node_modules/` at least (we won't look at import mappings for now)) return an empty object. (If importing `default`, return an empty object too.)
- Whack Red configures node-resolve `browser=true` during web builds.
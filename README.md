# remark-extract-toc

[remark](https://github.com/remarkjs/remark) plugin to store table of contents.

This plugin extracts only `Heading` from [mdast](https://github.com/syntax-tree/mdast) markdown, then converts them to a nested object tree keeping the depth.

# Install

```
npm install remark-extract-toc
```

# Usage

```
var unified = require("unified");
var markdown = require("remark-parse");
var toc = require("remark-extract-toc");

var fs = require("fs");
var text = fs.readFileSync("example.md", "utf8");

var processor = unified()
  .use(markdown, { commonmark: true })
  .use(toc);

var node = processor.parse(text);
var tree = processor.processSync(node);
console.log(tree);
```

This `example.md`

```
# Alpha

aaaa

## Bravo

bbbb

### Charlie

cccc

## Delta

dddd
```

will be converted by this library like...

```
[
  {
    depth: 1,
    value: "Alpha",
    children: [
      {
        depth: 2,
        value: "Bravo",
        children: [{ depth: 3, value: "Charlie", children: [] }],
      },
      {
        depth: 2,
        value: "Delta",
        children: [],
      },
    ],
  },
]
```

# License

MIT

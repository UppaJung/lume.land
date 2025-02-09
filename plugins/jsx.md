---
title: JSX
description: Create pages and layouts with JSX (React).
mod: plugins/jsx.ts
tags:
  - template_engine
---

## Description

[JSX](https://facebook.github.io/jsx/) (or the equivalent TSX for TypeScript) is
a template language to create and render HTML code, very popular in some
frameworks, like React. This plugin adds support for `JSX / TSX` to create pages
and layouts, using `React` for rendering.

## Installation

Import this plugin in your `_config.ts` file to use it:

```js
import lume from "lume/mod.ts";
import jsx from "lume/plugins/jsx.ts";

const site = lume();

site.use(jsx(/* Options */));

export default site;
```

### Configuration

You might want to add the following `compilerOptions` to `deno.json` in order to
configure the JSX transform:

<lume-code>

```json {title="deno.json"}
{
  // ...
  "compilerOptions": {
    "jsx": "react-jsx",
    "jsxImportSource": "npm:react",
    "types": [
      "lume/types.ts",
      "https://unpkg.com/@types/react@18.2.37/index.d.ts"
    ]
  }
}
```

</lume-code>

[Go to Using TypeScript](/docs/configuration/using-typescript/) for more info
about using TypeScript with Lume. {.tip}

## Creating pages

To create a page with this format, just add a file with `.jsx` or `.tsx`
extension to your site. This format works exactly the same as
[JavaScript/TypeScript files](./modules.md), but with the addition of the
ability to export JSX code in the default export:

```tsx
export const title = "Welcome to my page";
export const layout = "layouts/main.vto";

export default (data: Lume.Data, helpers: Lume.Helpers) => (
  <>
    <h1>{data.title}</h1>
    <p>This is my first post using lume. I hope you like it!</p>
  </>
);
```

Note that this page uses the `layouts/main.vto` layout to wrap the content (you
can mix different template languages like Nunjucks and JSX)

## Creating layouts

To create layouts in JSX, just add `.jsx` or `.tsx` files to the `_includes`
directory. Note that we need to use the variable `children` to render the page
content instead of `content`. The difference is that `content` is a string and
cannot be easily used in JSX because it's escaped, and `children` is the JSX
object un-rendered.

```tsx
export default ({ title, children }: Lume.Data, helpers: Lume.Helpers) => (
  <html>
    <head>
      <title>{title}</title>
    </head>
    <body>
      {children}
    </body>
  </html>
);
```

Lume will automatically add the missing `<!DOCTYPE html>` to the generated
`.html` pages. {.tip}

# API Next

This is an exploration of what could be next in API design tooling. Maybe the future tools we want are already here.

## The Issues

### Single File Formats

Most API description formats focus work around a single file. There are ways to break these files apart using JSON `$ref` or YAML references. However, these solutions are focused on JSON and YAML rather than allowing for modularity around API semantics.

### Mixing of Formats

API Blueprint allows for adding special syntax into Markdown and embedding other formats like JSON through block quotes and code blocks. OpenAPI allows for Markdown within JSON or YAML. In all of these solutions, formats are mixed together.

### Extensibility

Extensibility is limited in all formats. OpenAPI provides vendor extensions, but this focuses around the description format more than the tooling. It's much hard to build tools within the ecosystem, so most solutions are forced to be standalone.

## What's next?

The proposal here is to explore using Webpack and other technologies as an API design toolset. Webpack provides modularity and allows for the handling of many formats in a single place (e.g. JavaScript, HTML, and CSS).

### Develop and Build with Webpack

#### Dependency Graph

Webpack handles the dependency graph and provides modularity to any kind of file formats. This includes JavaScript, CSS, HTML, and other formats like images or JSON documents. This goes far beyond what JSON and YAML can do alone, even with existing ecosystems around those formats.

This dependency graph is the magic that Webpack brings. If used for designing APIs, it allows designers to divide up their work into files and formats that make sense and use CommonJS to manage dependencies. This not only gives a clear picture of the dependency graph, it allows for extensibility as new formats and tools can be installed via npm and included using CommonJS `require`.

#### Build Process

Webpack provides a build process that can take the graph of assets and create bundles. These bundles can consist of a single JavaScript file, a CSS processed by Sass, HTML processed by template formats, optimized images, or any other kind of asset.

Webpack's build process can be used to take many assets that are part of the API description and combine them into a final "compiled" document. This allows for users to write Markdown, JavaScript, JSON, or whatever, all separate from each other, and then build something together as a final asset. 

#### Development Tools

Webpack comes with powerful development tools and a development server to aid in the creation of these assets. Hot module replacement can be used to give immediate feedback to the designer on the validity and result of their designs. The development server can be used to provide mock request and responses. And testing tools can be used to ensure governance across the entire design.

### Code Rather Than DSL

API Blueprint and OpenAPI are both based around a DSL for describing APIs. However, as time goes on, these DSLs are unable to accommodate the needs of API designers. As the [complexity clock shows](http://mikehadlow.blogspot.com/2012/05/configuration-complexity-clock.html), it's almost time to move back to hard-coding things.

With Webpack, we can focus on writing code and using all of JavaScript to produce an API design.

#### Single File Components

Vue.js has a special loader for Webpack that allows for [Single File Components](https://vuejs.org/v2/guide/single-file-components.html). This file format allows for modularity while letting the developer use multiple technologies in one file. Since Webpack can solve modularity, it can also solve mixing formats together in a single file in a much better way. Please take a look at that technology along with the rationale for it to get an idea of how this would work.

Below is an example of a Customer resource as a single file component.

```
<documentation format="markdown">
# Customer

Here is where we would describe the customer resource in Markdown.
</documentation>

<script>
// This is where we would import other resources and compose things together.
// We would use plain JavaScript, Typescript, or use and define another
// format like JSON or YAML.
</script>
```

#### Optionally, JSX as Declarative Syntax

TypeScript has native JSX support and React can be used in a generic way with JSX, all of which could be used to write declarative specifications. This format could be used to define resources, to wire up resource defintions to protocols, to mix declarations with logic, or to even make it easy to write things like JSON Schema (e.g. `<object>` rather than `{"type":"object"}`).

## Affordance-Centric Rather than Resource-Centric

The proposal so far has revolved around API design tooling, however, this could be an opportunityt to explore creating technology for affordance-centric design. Affordance specifications could be grouped in a directory and imported into resources where applicable.

## Conclusion

This is all a tip of the iceberg of what could happen, but ultimately, it's a push toward a better environment for designing and developing APIs using existing tooling. This is a move away from config files and DSLs to using real code, leveraging things like CommonJS and patterns like Single File Components for Vue.js.
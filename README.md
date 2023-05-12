# react-d3-graph &middot; [![Build Status](https://github.com/danielcaldas/react-d3-graph/workflows/react-d3-graph/badge.svg)](https://github.com/danielcaldas/react-d3-graph/workflows/react-d3-graph/badge.svg)

[![npm version](https://img.shields.io/npm/v/react-d3-graph.svg?style=flat-square)](https://www.npmjs.com/package/react-d3-graph) [![npm](https://img.shields.io/npm/dw/react-d3-graph.svg?style=flat-square)](https://www.npmjs.com/package/react-d3-graph)
[![npm](https://img.shields.io/npm/dt/react-d3-graph.svg?style=flat-square)](https://www.npmjs.com/package/react-d3-graph) [![probot enabled](https://img.shields.io/badge/probot:stale-enabled-yellow.svg?longCache=true&style=flat-square)](https://probot.github.io/) [![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

:book: [Documentation](https://danielcaldas.github.io/react-d3-graph/docs/index.html)

### _Interactive and configurable graphs with react and d3 effortlessly_

[![react-d3-graph gif sample](https://github.com/danielcaldas/react-d3-graph/blob/master/sandbox/rd3g_v2.gif?raw=true)](https://danielcaldas.github.io/react-d3-graph/sandbox/index.html)

## Playground

[Here a live playground](https://danielcaldas.github.io/react-d3-graph/sandbox/index.html) page where you can interactively config your own graph, and generate a ready to use configuration! :sunglasses:

You can also load different data sets and configurations via URL query parameter. Below is a table with all the data sets available in the live sandbox for you to interactively explore different kinds of integrations with the library.

| Name   | Link                                                                                      | Source                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| :----- | :---------------------------------------------------------------------------------------- | :------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| small  | [demo](https://danielcaldas.github.io/react-d3-graph/sandbox/index.html?data=small)       | `sandbox/data/small`       | This is a good example to get you started. It has only 4 nodes. It's good to discuss over integration details and it's also good to report issues that you might found in the library. It's much easier to debug over a tiny graph.                                                                                                                                                                                                                                                                                   |
| custom | [demo](https://danielcaldas.github.io/react-d3-graph/sandbox/index.html?data=custom-node) | `sandbox/data/custom-node` | In this example you'll be able to see the power of the feature [node.viewGenerator](https://danielcaldas.github.io/react-d3-graph/docs/#node-view-generator) to create highly customizable nodes for you graph that go beyond the simple shapes that come out of the box with the library.                                                                                                                                                                                                                            |
| marvel | [demo](https://danielcaldas.github.io/react-d3-graph/sandbox/index.html?data=marvel)      | `sandbox/data/marvel`      | In this thematic example you can see how several features such as: [nodeHighlightBehavior](https://danielcaldas.github.io/react-d3-graph/docs/#node-highlight-behavior), [custom SVGs for nodes](https://danielcaldas.github.io/react-d3-graph/docs/#node-svg), [collapsible](https://danielcaldas.github.io/react-d3-graph/docs/#collapsible) etc. come together on top of a directed graph that displays some characters from the Marvel Universe.                                                                  |
| static | [demo](https://danielcaldas.github.io/react-d3-graph/sandbox/index.html?data=static)      | `sandbox/data/static`      | If your goal is not to have nodes dancing around with the default [d3 forces](https://danielcaldas.github.io/react-d3-graph/docs/#config-d3) that the library provides, you can opt by making your nodes static and positioned them always in the same _(x, y)_ coordinates. To achieve this you can make use of [staticGraphWithDragAndDrop](https://danielcaldas.github.io/react-d3-graph/docs/#static-graph-with-drag-and-drop) or [staticGraph](https://danielcaldas.github.io/react-d3-graph/docs/#static-graph) |

Do you want to visualize your own data set on the live sandbox? Just submit a PR! You're welcome 😁.

## Documentation :book:

Full documentation [here](https://danielcaldas.github.io/react-d3-graph/docs/index.html).

## Install

[![https://nodei.co/npm/YOUR-MODULE-NAME.png?downloads=true&downloadRank=true&stars=true](https://nodei.co/npm/react-d3-graph.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/react-d3-graph)

```bash
npm install d3@^5.5.0      # if you don't have d3 already
npm install react@^16.4.1  # if you don't have react already

npm install react-d3-graph
```

#### About react and d3 peer dependencies

**Note** that `react` and `d3` are [peer-dependencies](https://nodejs.org/en/blog/npm/peer-dependencies/), this means that the responsibility to install them is delegated to the client. This will give you more flexibility on what versions of `d3` and `react` you want to consume, you just need to make sure that you are compliant with the range of versions that `react-d3-graph` is compatible with. If you install `react-d3-graph` without first installing `d3` and `react` you might see the following warnings:

> npm WARN react-d3-graph@2.0.1 requires a peer of d3@^5.5.0 but none is installed. You must install peer dependencies yourself.
> npm WARN react-d3-graph@2.0.1 requires a peer of react@^16.4.1 but none is installed. You must install peer dependencies yourself.

## Minimal usage example

Graph component is the main component for react-d3-graph components, its interface allows its user to build the graph once the user provides the data, configuration (optional) and callback interactions (also optional).
The code for the [live example](https://danielcaldas.github.io/react-d3-graph/sandbox/index.html) can be consulted [here](https://github.com/danielcaldas/react-d3-graph/blob/master/sandbox/Sandbox.jsx).

```javascript
import { Graph } from "react-d3-graph";

// graph payload (with minimalist structure)
const data = {
  nodes: [{ id: "Harry" }, { id: "Sally" }, { id: "Alice" }],
  links: [
    { source: "Harry", target: "Sally" },
    { source: "Harry", target: "Alice" },
  ],
};

// the graph configuration, just override the ones you need
const myConfig = {
  nodeHighlightBehavior: true,
  node: {
    color: "lightgreen",
    size: 120,
    highlightStrokeColor: "blue",
  },
  link: {
    highlightColor: "lightblue",
  },
};

const onClickNode = function(nodeId) {
  window.alert(`Clicked node ${nodeId}`);
};

const onClickLink = function(source, target) {
  window.alert(`Clicked link between ${source} and ${target}`);
};

<Graph
  id="graph-id" // id is mandatory
  data={data}
  config={myConfig}
  onClickNode={onClickNode}
  onClickLink={onClickLink}
/>;
```




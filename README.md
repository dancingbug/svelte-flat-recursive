# svelte-flat-recursive

## what
A small svelte (higher-order) component for using a ES2015 `Map` with elements linked by `parent-id` fields to easily create recursively-nested components

## why
Normally in demos for Svelte component recursion, the structure of the data matches the structure of the rendered DOM.
This can be inconvenient, say for instance if the data are coming from a relational database as a flat list of nodes.
Underneath the hood, this component does the structure-nesting for you

## running the example
```
cd [clone directory]
npm install
npm run dev
```

## usage
1. Create a new Map()
1. use tree_helpers:map_set(...) to set nodes
1. use tree_helpers:sync_tree(...) after making changes
1. place a `RecTreeHost` in your component. Props:
    - `component_type`: your custom component. it must expose a slot called "recurse" and a prop "tree_data"
    - `root_ids`: an array of nodes to display in the root of the tree container
    - `node_map`: the map containing your elements

see `src/sample/Sample.svelte`

## contributing
Please feel free to open an issue or discussion if you have any suggestions.

## potential improvements
1. performance
    - probably there are a lot of unnecessary iterations and copies taking place.
    - I wonder if there is a more performant solution than keeping a child_ids array for each tree node.
      Unfortunately something like this seems necessary for svelte's `{#each}`
1. customization
    - allow customization of prop/slot names 
1. other data structures
    - create an API for using anything that can be indexed by node id
    - generalize child_ids store to use anything `{#each}`-able
1. virtual views
    - a mechanism to only show portions of the tree, or only a few levels at a time

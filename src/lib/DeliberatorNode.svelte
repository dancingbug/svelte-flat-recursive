<script>
  import { onMount } from 'svelte';
  export let tree_node;
  export let get_this;
  export let reply;

  function add_subnode() {
    tree_node.subnodes.unshift( {id: 100, content: "foo", subnodes: []});
    tree_node.subnodes = tree_node.subnodes;
    console.log(JSON.stringify(tree_node));
  };

  let content;
</script>


<div class="component">

  <div class="content">


    {tree_node.content}, id: {tree_node.id}
    <div class="actions">
      <div bind:this={reply} on:click={add_subnode}>new reply</div>
      <div class="merge">propose merge...</div>
    </div>

  </div>

  <div class="sub">
    {#each tree_node.subnodes as subnode}
      <svelte:self tree_node={subnode} />
    {/each}
  </div>
</div>

<style>
  .content {
    padding:10px;
    border: solid 1px black;
    text-align:left;
  }
  .editor {
    padding: 10px;
    border: 2px solid black;
    border-radius:8px;
  }
  #submit {
    cursor: pointer;
  }
  .sub {
    margin-left:30px;
  }
  .actions {
    display:flex;
    width:100%;
    gap:10px;
  }
  .actions > * {
    box-sizing:content-box;
    margin:0;
    font-size:0.8em;
    background-color: #EEEEFF;
    padding:2px;
    text-align:center;
  }
  .actions > *:hover {
    font-weight:bold;
  }

</style>



<script>
	import { setContext } from 'svelte';
  import DeliberatorNode from './DeliberatorNode.svelte'
  import DeliberatorNodeInserter from './DeliberatorNodeInserter.svelte'

  
  let nodectr;
  let items = [];
  
  let items2 = [
    {
      id: 0,
      content: "first",
      subnodes: []
    },
    {
      id:7,
      content: "second",
      subnodes: []
    },
    {
      id:8,
      content: "third",
      subnodes: []
    }
  ];

  
  let inserting_toplevel_argpoint;

  function insert_point(parent_id_) {
    //fetch('http://localhost:3000/api/argument_item', {
    //  method: 'POST',
    //  body: JSON.stringify({
    //    parent_id: parent_id_
    //  })
    //}).then(
    //  (resp) => {
    //    items.push()

    //    
    //    
    //})
    
  }

  function merge_points(list, primary) {
    
  }

  function insert_argpoint(tgt) {
    if (tgt === null) {
      return;
    }

    const argpoint_elem_inserting = new DeliberatorNodeInserter({
      target: tgt,
      anchor: tgt.firstChild,
      hydrate:false,
      props: {
        docancel: () => {argpoint_elem_inserting.$destroy()},
        dosubmit: () => {},
      }

    });

  }

  function toggle_inserting() {
    inserting_toplevel_argpoint = !inserting_toplevel_argpoint;
  }

</script>

<div class="component">
  <div class="flex-apart">
    <h1>argument items</h1>
    <div class="juicy-button"><button on:click={toggle_inserting}>(+/-)</button></div>
  </div>
  <div class="{inserting_toplevel_argpoint ? 'hidden' : ''}">
    <DeliberatorNodeInserter dosubmit={() => {}} docancel={() =>{toggle_inserting()}}/>
  </div>
  <div bind:this={nodectr}>
  {#each items as tree_node }
    <DeliberatorNode tree_node={tree_node}/>
  {/each}
  </div>
</div>

<style>
  .component {
    border: solid 1px black;
    padding:10px;
    margin:0;
    width: 90vw;
    box-sizing:border-box;
    text-align:left;
  }
  .component h1 {
    font-size: 1.5rem;
    margin:14px 0 14px 0;
    padding:0;
  }
  .hidden {
    display:none;
  }
  .flex-apart {
    display:flex;
  }
  .juicy-button {
    position:relative;
    margin:14px 0 14px 10px;
    font-weight:bold;
  }
  .juicy-button > span {
    display:block;
    position:absolute;
    bottom:0;
    cursor:pointer;
  }
</style>

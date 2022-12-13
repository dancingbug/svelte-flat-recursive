<script>
	import { setContext,getContext } from 'svelte';
  import DeliberatorNode from './DeliberatorNode.svelte'
  import DeliberatorNodeInserter from './DeliberatorNodeInserter.svelte'

  


  items = 
  [
    [1,null,'content 1']
    ,[2,null,'content 2']
    ,[3,2,'content 3']
    ,[4,1,'content 4']
  ];






  let is_inserting_toplevel_node;
  let item_container
  
  setContext('argument_points', new Map());
  let argpts = getContext('argument_points');

  setContext('node_callbacks', {
    append: async (parent_id, content) => {
      if (content === null) {
        //TODO
        //invalid input
        return
      }
      await insert_point(parent_id, content)
    }
  })


  setContext('inserter_callbacks', {
    append: async (parent_id, contents_) => {
      await insert_point(parent_id,contents_)
    },
    merge: (id) => {},
    getcontent: (id) => {}
  })




  function register_id(map, node_id, elem) {
    map.set(node_id, elem);
  }

  async function insert_point(parent_id_, content_) {
  
    let parent_elem = argpts.get('parent_id_');
    
    



    let resp = 
      await fetch('http://localhost:3000/api/argument_item', {
        method: 'POST',
        body: JSON.stringify({
          parent_id: parent_id_,
          content: content_
        })
      })

    if (!resp.ok) {
      console.log("not ok")
      return;
    }
    //should use background syncing instead somehow

    if (parent_id_ === null) {
      //add to top-level
      insert_node(item_container, {data:{id: resp.rowid,content:content_}});
    }
    else {
    //  insert_node(argpts.get(parent_id), {data:{resp.rowid}});
      console.log(argpts.get(parent_id_));
    }

  }

  function merge_points(list, primary) {
    
  }

  function destroy_node(id) {
    
  }
  function insert_node(tgt,nodeData) {
    if (tgt === null) {
      return;
    }

    const inserting_node = new DeliberatorNode({
      target: tgt,
      anchor: tgt.firstChild,
      hydrate:false,
      props: {
        ...nodeData 
      }

    });

  }

  function insert_nodeinserter(tgt,nodeData) {
    if (tgt === null) {
      return;
    }

    const inserting_node = new DeliberatorNodeInserter({
      target: tgt,
      anchor: tgt.firstChild,
      hydrate:false,
      props: {
        ...nodeData 
      }

    });

  }

  function toggle_inserting() {
    is_inserting_toplevel_node = !is_inserting_toplevel_node;
  }

</script>

<div class="component">

  <div class="flex-apart">
    <h1>argument items</h1>
    <button class="juicy-button" on:click={toggle_inserting}>+ / &minus</button>
  </div>

  <div class="{is_inserting_toplevel_node ? 'hidden' : ''}">
    <DeliberatorNodeInserter parent_id={null} docancel={() =>{toggle_inserting()}}/>
  </div>


  <div bind:this={item_container}>
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
    display:block;
  }
  .hidden {
    display:none;
  }
  .flex-apart {
    display:flex;
    gap:20px;
  }
  .juicy-button {
    background-color: #EEEEFF;
    border: 1px solid black;
    display:block;
    margin:14px 0 14px 0px;
    padding:6px;
    font-weight:bold;
  }
</style>

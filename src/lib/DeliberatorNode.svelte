<script>
  import { getContext,onMount } from 'svelte';
  export let data
  export let child_container
  const map = getContext('argument_points')

  const callbacks = getContext('node_callbacks')  


   


</script>


<div class="component">

  <div class="content">

    id: {data.id}
    content: {data.content}

    <div class="actions">
      <div on:click={callbacks.append(data.id)}>new reply</div>
      <div on:click={callbacks.merge(data.id)}>propose merge...</div>
    </div>

  </div>

  <div bind:this={child_container} class="sub">
    
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



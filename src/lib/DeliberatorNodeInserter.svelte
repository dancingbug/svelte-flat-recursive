<script>
  import { getContext, onMount } from 'svelte';

  export let parent_id = null
  export let docancel = () => {};
  let content;

  

  const cb = getContext('inserter_callbacks');

  async function append() {
    cb.append(parent_id,content)
  }
  async function cancel() {
    docancel()
  }

</script>


<div class="component">

  <div class="content">
    <h1 class="title">New entry</h1>
    <input bind:value={content} class="editor" name="new_entry" placeholder="edit me" />
    <div class="actions">
      <div id="submit" class="pointer" on:click={append}>submit</div>
      <div id="cancel" class="pointer" on:click={cancel}>cancel</div>
    </div>


  </div>

</div>

<style>
  .title {
    font-size: 1.5rem;
  }
  .content {
    padding:10px;
    border: solid 1px black;
    text-align:left;
  }
  .editor {
    box-sizing:border-box;
    padding: 10px;
    border: 2px solid black;
    border-radius:8px;
    display:block;
    width:100%;
  }
  .pointer {
    cursor: pointer;
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



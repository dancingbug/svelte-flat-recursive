<script>
  import { onMount } from 'svelte';
  export let dosubmit;
  export let docancel;

  let content;
</script>


<div class="component">

  <div class="content">
    <h1 class="title">New entry</h1>
    <div class="editor" contenteditable="true" bind:textContent={content}>
      edit me!
    </div>
    <div class="actions">
      <div id="submit" class="pointer" on:click={dosubmit()}>submit</div>
      <div id="cancel" class="pointer" on:click={docancel()}>cancel</div>
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
    padding: 10px;
    border: 2px solid black;
    border-radius:8px;
  }
  .pointer {
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



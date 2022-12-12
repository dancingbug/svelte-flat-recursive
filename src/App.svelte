<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import Connect from './lib/Connect.svelte'
  import Counter from './lib/Counter.svelte'
  import MyCanvas from './lib/MyCanvas.svelte'
  import DeliberatorTree from './lib/DeliberatorTree.svelte'
</script>

<main>
  <div class="float-upper-right">
    <Connect />
  </div>

  <h1>Vite + Svelte</h1>


  <DeliberatorTree/>

  <div class="card">
   <MyCanvas />
  </div>


  <div class="card">
    <Counter />
  </div>

</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
  .float-upper-right {
    float:right;
  }
</style>

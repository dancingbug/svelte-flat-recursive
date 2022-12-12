<script>
import { onMount } from 'svelte';
let userfield;
let saw_error;
saw_error = false;
function validateEmail(e) {
  if (userfield.value == "") {
    saw_error = true;
    console.log("enter a username/email!");
  }
  saw_error = false;
  e.preventDefault();

}

</script>



<form class="loginform">
  <div class:input-error="{saw_error}">akflsakf;sa<div>
  <input class:input-error="{saw_error}" bind:this={userfield} name="user" type="text" placeholder="username/email"/>
  <button on:click={validateEmail}>login</button>
</form>


<style>
  .input-error {
    border:2px solid red;
  }
</style>






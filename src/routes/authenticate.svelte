<script>
  import { navigate } from 'svelte-routing';

  let enteredPin = Array(4).fill(null);
  let storedPin = JSON.parse(localStorage.getItem('pinColors'));

  function enterPin(index, color) {
    enteredPin[index] = color;
  }

  function authenticate() {
    // Check if enteredPin matches storedPin
    if (JSON.stringify(enteredPin) === JSON.stringify(storedPin)) {
      alert("Pin authenticated!");
      // Navigate to success page or perform further actions
    } else {
      alert("Incorrect pin. Please try again.");
    }
  }
</script>

<h1>Enter Your Pin to Authenticate</h1>

<div class="color-selector">
  {#each enteredPin as color, index}
    <div
      class="color-square"
      style="background-color: {color || 'gray'}"
      on:click={() => enterPin(index, color)}
    ></div>
  {/each}
</div>

<button on:click={authenticate}>Authenticate</button>

<style>
  .color-selector {
    display: flex;
    justify-content: space-around;
  }

  .color-square {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    margin: 10px;
    cursor: pointer;
  }
</style>

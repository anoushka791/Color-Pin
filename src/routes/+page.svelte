<script>
  import { navigate } from 'svelte-routing';

  // Define the available color options
  let colorOptions = [
    ["#ADDFFF", "#306EFF", "#357EC7"],
    ["#1AA260", "#00A36C", "#347C2C"],
    ["#FFA62F", "#E9AB17", "#F87217"],
    ["#F67280", "#D58A94", "#E56E94"],
    ["#9D00FF", "#8467D7", "#B041FF"],
    ["#660000", "#3D0C02", "#560319"]
  ];

  // Initialize selected colors with null values
  let selectedColors = Array(4).fill(null);

  // Function to select a color for a specific index
  function selectColor(index, color) {
    selectedColors[index] = color;
  }

  // Function to proceed to the authentication page
  function proceed() {
    // Check if all pins are selected
    if (selectedColors.every(color => color !== null)) {
      // Store selectedColors in localStorage or send to backend
      localStorage.setItem('pinColors', JSON.stringify(selectedColors));
      navigate('/authenticate');
    } else {
      alert("Please select all pin colors.");
    }
  }
</script>

<h1>Select Your 4 Colored Pin</h1>

<div class="color-selector">
  {#each colorOptions as option}
    {#each option as color}
      <div
        class="color-square {selectedColors[selectedColors.indexOf(null)] !== null ? 'selected' : ''}"
        style="background-color: {color}"
        on:click={() => selectColor(selectedColors.indexOf(null), color)}
      ></div>
    {/each}
  {/each}
</div>

<button on:click={proceed}>Proceed</button>

<style>
  .color-selector {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .color-square {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    margin: 10px;
    cursor: pointer;
  }

  .selected {
    opacity: 0.5; /* Adjust opacity to visually indicate selected color */
  }
</style>

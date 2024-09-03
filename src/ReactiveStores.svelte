<script>
    import { writable } from 'svelte/store';

    let inputData = writable([10, 20, 30, 100, 40, 60]);
    let newValue = 0;

    // Function to add data safely
    function addData() {
        if (newValue !== '' && !isNaN(newValue)) {
            inputData.update(n => [...n, parseInt(newValue)]);
            newValue = 0;  // Reset the input value after adding
        }
    }
</script>

<!-- User Interface -->
<div>
    <input type="number" bind:value={newValue} min="0" placeholder="Enter value" />
    <button on:click={addData}>Add Data</button>
</div>

<!-- Visualization -->
<svg width="100&" height="300"> <!-- Adjusted height for better visibility -->
    {#each $inputData as d, i}
        <rect x={i * 50 + 10} y={300 - d} width="40" height={d} fill="steelblue" />
        <!-- Label each bar with its value -->
        <text x={i * 50 + 30} y={300 - d - 5} fill="white" text-anchor="middle">{d}</text>
    {/each}
</svg>

<style>
    input, button {
        padding: 8px;
        margin: 5px;
        font-size: 16px;
    }
    button {
        cursor: pointer;
    }
</style>
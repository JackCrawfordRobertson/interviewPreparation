<script>
    import { writable } from 'svelte/store';

    // Create a writable store for currentStep
    let currentStep = writable(0);

    let data = [
	        { year: 2000, value: 400 },
        { year: 2005, value: 200 },
        { year: 2010, value: 300 },
    ];

    // Function to handle keyboard events
    function handleKeyDown(event, index) {
        if (event.key === 'Enter' || event.key === ' ') {
            currentStep.set(index); // Update the store
            event.preventDefault(); // Prevent the default scroll behavior for space
        }
    }
</script>

<style>
    .scroll-container {
        display: flex;
        justify-content: space-around;
        background-color: #f0f0f0; /* Light gray background */
        padding: 10px;
        border-radius: 8px;
				min-height: 100px;
    }

    .step {
        cursor: pointer;
        padding: 10px;
        margin: 0 10px;
        border-radius: 8px;
        transition: transform 0.2s, background-color 0.2s;
        background-color: #fff; /* White background for each box */
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Subtle shadow */
        flex: 1;
        text-align: center; /* Center text within each step */
    }

    .step:hover,
    .step:focus {
        transform: scale(1.05);
        background-color: #e0e0e0; /* Slightly darker gray for hover */
    }

    svg {
        display: block;
        margin: 20px auto;
    }
</style>

<div class="scroll-container">
    {#each data as d, i}
        <div 
            class="step" 
            role="button" 
            tabindex="0"
            on:click={() => currentStep.set(i)} 
            on:keydown={(event) => handleKeyDown(event, i)}
        >
            <h2>Year: {d.year}</h2>
            <p>Value: {d.value}</p>
        </div>
    {/each}
</div>

	<svg width="auto" height="auto" viewBox="0 0 500 200">
    <circle cx={$currentStep * 30 + 90} cy="100" r="70" fill="teal" />
</svg>
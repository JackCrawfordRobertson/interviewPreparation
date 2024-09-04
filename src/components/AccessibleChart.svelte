<!-- AccessibleChart.svelt -->
<script>
    let data = [10, 20, 30];
    let maxDataValue = Math.max(...data); // Calculate the maximum data value for scaling the y-axis

    // Function to handle keyboard events more comprehensively
    function handleKeyDown(e, i) {
        if (e.key === 'Enter' || e.key === ' ') { // Respond to both Enter and Space
            alert(`You selected bar ${i + 1} with value ${data[i]}`);
            e.preventDefault(); // Prevent the default action for spacebar
        }
    }
</script>

<svg width="400" height="240" role="img" aria-label="Bar chart of values 10, 20, 30">
    <!-- Y Axis -->
    <line x1="70" y1="200" x2="70" y2="10" stroke="black"/> <!-- Shifted right for padding -->
    <!-- X Axis -->
    <line x1="70" y1="200" x2="350" y2="200" stroke="black"/> <!-- Start also shifted for consistent padding -->

    {#each data as d, i}
        <rect
            x={70 + i * 100 + 30} 
            y={200 - (d * 180 / maxDataValue)} 
            width="40"
            height={d * 180 / maxDataValue} 
            tabindex="0"
            role="button"
            aria-label={`Bar ${i + 1}: value ${d}`}
            on:keydown={(e) => handleKeyDown(e, i)}
            fill="purple"
            style="outline: none;"
        />
        <!-- Labels for the x-axis -->
        <text x={120 + i * 100} y="215" fill="black" text-anchor="middle"> <!-- Adjusted label positioning -->
            {`Year ${2000 + 5 * i}`}
        </text>
    {/each}

    <!-- Adding labels for the y-axis at significant points -->
    {#each Array(5) as _, i} <!-- Create 5 labels evenly distributed -->
        <text x="65" y={200 - i * 45} fill="black" text-anchor="end">
            {Math.round(i * (maxDataValue / 4))} <!-- Round to avoid fractional numbers -->
        </text>
    {/each}
</svg>

<style>
    text {
        font-family: 'Arial', sans-serif;
        font-size: 12px;
    }
</style>
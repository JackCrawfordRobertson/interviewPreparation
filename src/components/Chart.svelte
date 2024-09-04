<script>
  import { onMount } from 'svelte';
  import Plotly from 'plotly.js-dist-min';

  let chartContainer;

  onMount(() => {
    const data = [{
      x: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
      y: [12, 19, 3, 5, 2, 3],
      type: 'bar',
      marker: {
        color: ['rgba(255, 99, 132, 0.6)', 'rgba(54, 162, 235, 0.6)', 
                'rgba(255, 206, 86, 0.6)', 'rgba(75, 192, 192, 0.6)', 
                'rgba(153, 102, 255, 0.6)', 'rgba(255, 159, 64, 0.6)'], // Custom colors for each bar
        line: {
          color: ['rgba(255, 99, 132, 1)', 'rgba(54, 162, 235, 1)', 
                  'rgba(255, 206, 86, 1)', 'rgba(75, 192, 192, 1)', 
                  'rgba(153, 102, 255, 1)', 'rgba(255, 159, 64, 1)'],
          width: 1.5 // Border width of the bars
        }
      }
    }];

    const layout = {
      title: 'Colorful Bar Chart',
      font: { family: "Lato, sans-serif", size: 16, color: "#333" },
      titlefont: { size: 24 },
      xaxis: {
        title: 'Colors',
        titlefont: { size: 18 },
        tickfont: { size: 14 }
      },
      yaxis: {
        title: 'Number of Votes',
        titlefont: { size: 18 },
        tickfont: { size: 14 }
      },
      margin: { t: 60, l: 50, r: 50, b: 50 }, // Margin around the chart
      paper_bgcolor: 'white', // Background color of the plotting area
      plot_bgcolor: 'white', // Background color of the chart itself
      showlegend: false
    };

    Plotly.newPlot(chartContainer, data, layout);

    return () => {
      Plotly.purge(chartContainer); // Clean up when the component is destroyed
    };
  });
</script>

<div bind:this={chartContainer} style="width: 100%; height: 400px;"></div>
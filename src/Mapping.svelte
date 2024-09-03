<script>
    import { onMount } from 'svelte';
    import mapboxgl from 'mapbox-gl'; // Import Mapbox GL JS

    let map;
    let mapContainer;
    let showLayer = true; // Declare showLayer and set its initial value
    let popup = new mapboxgl.Popup({
        closeButton: false,
        closeOnClick: false
    });

    mapboxgl.accessToken = 'pk.eyJ1IjoiamltYm9ic3RldmUyMTIzIiwiYSI6ImNraDZuYzVmMTBleWkycnFjdG9mOTJyeXEifQ.roRb52vy53cHa03UXhnIUA'; // Replace with your Mapbox token

    onMount(() => {
        map = new mapboxgl.Map({
            container: mapContainer,
            style: 'mapbox://styles/jimbobsteve2123/ckh6ngljf1eqr19k6uvmrhncp', 
            center: [-0.1276, 51.5074], 
            zoom: 12
        });

        // Use the 'load' event to ensure the map is fully ready before adding layers
        map.on('load', () => {
            map.addLayer({
                id: 'points',
                type: 'circle',
                source: {
                    type: 'geojson',
                    data: {
                        type: 'FeatureCollection',
                        features: [
                            {
                                type: 'Feature',
                                geometry: {
                                    type: 'Point',
                                    coordinates: [-0.1276, 51.5074],
                                },
                                properties: {
                                    title: 'London'
                                }
                            },
                            {
                                type: 'Feature',
                                geometry: {
                                    type: 'Point',
                                    coordinates: [-0.1425, 51.5155],
                                },
                                properties: {
                                    title: 'Hyde Park'
                                }
                            },
                            {
                                type: 'Feature',
                                geometry: {
                                    type: 'Point',
                                    coordinates: [-0.0761, 51.5081], 
                                },
                                properties: {
                                    title: 'Tower of London'
                                }
                            },
                            {
                                type: 'Feature',
                                geometry: {
                                    type: 'Point',
                                    coordinates: [-0.1246, 51.5033], 
                                },
                                properties: {
                                    title: 'Westminster'
                                }
                            }
                        ]
                    }
                },
                paint: {
                    'circle-radius': 10,
                    'circle-color': '#007cbf'
                }
            });

            // Toggle the layer visibility based on showLayer
            map.setLayoutProperty('points', 'visibility', showLayer ? 'visible' : 'none');

            // Add hover interaction to display tooltips
            map.on('mouseenter', 'points', (e) => {
                // Change the cursor style as a UI indicator.
                map.getCanvas().style.cursor = 'pointer';

                // Get the coordinates and title from the feature
                const coordinates = e.features[0].geometry.coordinates.slice();
                const title = e.features[0].properties.title;

                // Ensure the popup is displayed at the correct place
                while (Math.abs(e.lngLat.lng - coordinates[0]) > 180) {
                    coordinates[0] += e.lngLat.lng > coordinates[0] ? 360 : -360;
                }

                // Set the popup content and display it
                popup
                    .setLngLat(coordinates)
                    .setHTML(`<strong>${title}</strong>`)
                    .addTo(map);
            });

            map.on('mouseleave', 'points', () => {
                map.getCanvas().style.cursor = ''; 
                popup.remove(); 
            });
        });
    });
</script>

<!-- Include the Mapbox CSS for proper map rendering -->
<link
    href="https://api.mapbox.com/mapbox-gl-js/v2.15.0/mapbox-gl.css"
    rel="stylesheet"
/>

<label>
    <input type="checkbox" bind:checked={showLayer} />
    Show Layer
</label>

<div bind:this={mapContainer} style="min-width: '100%'; height: 400px;"></div>

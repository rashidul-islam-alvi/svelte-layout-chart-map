<script>
  import { onMount } from "svelte";
  import { countryDataStore } from "../store/store";
  import { Chart } from "chart.js/auto";

  /**
   * @type {any[]}
   */
  let countries = [];

  /**
   * @type {HTMLCanvasElement | null}
   */
  let canvas = null;

  /**
   * @type {Chart<"polarArea", any[], any> | null}
   */
  let chart = null;

  // Observe changes in the countryDataStore
  $: {
    countries = $countryDataStore
      .slice()
      .sort((a, b) => b.population - a.population)
      .slice(0, 10)
      .map((country) => ({
        name: country.name.common,
        population: country.population,
      }));
  }

  onMount(() => {
    if (canvas) {
      const ctx = canvas.getContext("2d");

      if (ctx) {
        if (chart) {
          chart.destroy(); // Destroy the previous chart if it exists
        }

        chart = new Chart(ctx, {
          type: "polarArea",
          data: {
            datasets: [
              {
                data: countries.map((country) => country.population),
                backgroundColor: [
                  "rgba(255, 99, 132, 0.7)",
                  "rgba(255, 159, 64, 0.7)",
                  "rgba(75, 192, 192, 0.7)",
                  "rgba(54, 162, 235, 0.7)",
                  "rgba(153, 102, 255, 0.7)",
                  "rgba(255, 206, 86, 0.7)",
                  "rgba(255, 0, 0, 0.7)",
                  "rgba(0, 128, 0, 0.7)",
                  "rgba(0, 0, 255, 0.7)",
                  "rgba(255, 0, 255, 0.7)",
                ],
              },
            ],
            labels: countries.map((country) => country.name),
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: {
              r: {
                min: 0, // Customize the scale based on your data
              },
            },
          },
        });
      }
    }
  });
</script>

<main class="bg-white border-2">
  <div class="p-5 mb-5 text-xl font-bold border-b-2">Countries</div>
  <div class="my-10">
    <canvas bind:this={canvas} />
  </div>
</main>

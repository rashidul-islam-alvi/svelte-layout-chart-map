<script>
  import { onMount } from "svelte";
  import { countryDataStore } from "../../store/store";
  import Table from "../../components/Table.svelte";
  import PolarAreaChart from "../../components/PolarAreaChart.svelte";

  onMount(async () => {
    try {
      const response = await fetch("https://restcountries.com/v3.1/all");
      const data = await response.json();
      countryDataStore.set(data);
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  });
</script>

<main class="p-20 bg-gray-200 md:flex gap-x-10">
  <div class="flex-[5]"><Table /></div>
  <div class="flex-[2]"><PolarAreaChart /></div>
</main>

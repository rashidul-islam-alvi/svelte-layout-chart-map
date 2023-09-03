<script>
  import { countryDataStore } from "../store/store";

  /**
   * @type {any[]}
   */
  let countries = [];

  // Observe changes in the countryDataStore
  $: {
    countries = $countryDataStore;
  }
</script>

<main class="text-center">
  <table>
    <thead>
      <tr>
        <th>Flag</th>
        <th>Name</th>
        <th>CIOC</th>
        <th>UN Member Status</th>
        <th>Currencies (Key)</th>
        <th>Population</th>
        <th>Languages</th>
      </tr>
    </thead>
    <tbody>
      {#each countries as country}
        <tr>
          <td class="flex items-center justify-center">
            <img src={country.flags.png} alt={country.flags.alt} width="30" />
          </td>
          <td>{country.name.common}</td>
          <td
            >{#if country.cioc} {country.cioc} {:else} N/A{/if}</td
          >
          <td>{country.status === "officially-assigned" ? "Yes" : "No"}</td>
          <td>
            {#if country.currencies}
              {#each Object.keys(country.currencies) as currencyKey, index}
                {currencyKey}
                {#if index < Object.keys(country.currencies).length - 1}, {/if}
              {/each}
            {:else}
              N/A
            {/if}
          </td>
          <td>{country.population}</td>
          <td>
            {#if country.languages}
              {#each Object.values(country.languages).slice(0, 2) as language, index}
                {language}
                {#if index < Object.values(country.languages).length - 1}, {/if}
              {/each}
            {:else}
              N/A
            {/if}
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
</main>

<style>
  table {
    background-color: white;
    width: 100%;
    border-collapse: collapse;
  }

  tr {
    display: flex;
  }

  th,
  td {
    flex: 1;
    border: 1px solid #ccc;
    padding: 8px;
    text-align: center;
  }

  img {
    max-width: 100%;
    height: auto;
  }
</style>

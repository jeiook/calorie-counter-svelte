<script lang="ts">
  import CalorieNumberInput from "./CalorieInput/CalorieNumberInput.svelte";

  export let name: string;

  type Entry = { entryNumber: number; inputEl: CalorieNumberInput | null };
  let entries: Entry[] = [];

  function addEntry() {
    if (entries.length === 0) {
      entries = [{ entryNumber: 1, inputEl: null }];
      return;
    }
    entries = [
      ...entries,
      {
        entryNumber: entries[entries.length - 1].entryNumber + 1,
        inputEl: null,
      },
    ];
  }

  export function getCaloriesSum() {
    let calories = 0;
    for (const entry of entries) {
      if (!entry.inputEl) continue;
      calories += entry.inputEl.getCalories();
    }
    return calories;
  }
</script>

<fieldset id={name}>
  <legend>{name}</legend>
  <div class="input-container">
    {#each entries as { entryNumber, inputEl } (entryNumber - 1)}
      <label for="${name}-${entryNumber}-name">Entry {entryNumber} Name</label>
      <input type="text" id="${name}-${entryNumber}-name" placeholder="Name" />
      <CalorieNumberInput bind:this={inputEl} {name} order={entryNumber} />
    {/each}
  </div>
  <button on:click={addEntry} type="button" id="add-entry">Add Entry</button>
</fieldset>

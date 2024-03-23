<script lang="ts">
  import CalorieNumberInput from "./CalorieInput/CalorieNumberInput.svelte";

  export let name: string;

  type Entry = { entryNumber: number; calorieValue: number };
  let entries: Entry[] = [];

  function addEntry() {
    if (entries.length === 0) {
      entries = [{ entryNumber: 1, calorieValue: 0 }];
      return;
    }
    entries = [
      ...entries,
      {
        entryNumber: entries[entries.length - 1].entryNumber + 1,
        calorieValue: 0,
      },
    ];
  }

  export function getCaloriesSum() {
    let calories = 0;
    for (const { calorieValue } of entries) {
      if (!calorieValue) continue;
      calories += calorieValue;
    }
    return calories;
  }

  export function clearEntries() {
    entries = [];
  }

  const updateCalorieValue = (
    e: CustomEvent<{ calories: number }>,
    index: number
  ) => {
    entries[index] = { ...entries[index], calorieValue: e.detail.calories };
  };
</script>

<fieldset id={name}>
  <legend>{name}</legend>
  <div class="input-container">
    {#each entries as { entryNumber }, index (entryNumber - 1)}
      <label for="${name}-${entryNumber}-name">Entry {entryNumber} Name</label>
      <input type="text" id="${name}-${entryNumber}-name" placeholder="Name" />
      <CalorieNumberInput
        on:newInput={(e) => updateCalorieValue(e, index)}
        {name}
        order={entryNumber}
      />
    {/each}
  </div>
  <button on:click={addEntry} type="button" id="add-entry">Add Entry</button>
</fieldset>

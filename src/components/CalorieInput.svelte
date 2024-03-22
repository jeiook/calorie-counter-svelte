<script lang="ts">
  export let name: string;

  let entries: number[] = [];

  function addEntry() {
    if (entries.length === 0) {
      entries = [1];
      return;
    }
    entries = [...entries, entries[entries.length - 1] + 1];
  }
</script>

<fieldset id={name}>
  <legend>{name}</legend>
  <div class="input-container">
    {#each entries as entry}
      <label for="${name}-${entry}-name">Entry {entry} Name</label>
      <input type="text" id="${name}-${entry}-name" placeholder="Name" />
      <label for="${name}-${entry}-calories">Entry {entry} Calories</label>
      <input
        type="number"
        min="0"
        placeholder="Calories"
        id="${name}-${entry}-calories"
      />
    {/each}
  </div>
  <button on:click={addEntry} type="button" id="add-entry">Add Entry</button>
</fieldset>

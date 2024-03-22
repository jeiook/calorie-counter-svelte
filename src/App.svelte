<script lang="ts">
  import CalorieInput from "./components/CalorieInput.svelte";

  let calorieCounter: HTMLElement;
  let budgetNumberInput: HTMLElement;
  let clearButton: HTMLElement;
  let output: HTMLElement;

  let isError = false;

  const calorieInputCategories = [
    "breakfast",
    "lunch",
    "dinner",
    "snacks",
    "exercise",
  ];

  function cleanInputString(str: string) {
    const regex = /[+-\s]/g;
    return str.replace(regex, "");
  }

  function isInvalidInput(str: string) {
    const regex = /\d+e\d+/i;
    return str.match(regex);
  }
</script>

<main>
  <h1>Calorie Counter</h1>
  <div class="container">
    <form bind:this={calorieCounter} id="calorie-counter">
      <label for="budget">Budget</label>
      <input
        bind:this={budgetNumberInput}
        type="number"
        min="0"
        id="budget"
        placeholder="Daily calorie budget"
        required
      />

      {#each calorieInputCategories as category}
        <CalorieInput name={category} />
      {/each}

      <div>
        <button type="submit">Calculate Remaining Calories</button>
        <button bind:this={clearButton} type="button" id="clear">Clear</button>
      </div>
    </form>
    <div bind:this={output} id="output" class="output hide"></div>
  </div>
</main>

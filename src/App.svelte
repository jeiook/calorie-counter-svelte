<script lang="ts">
  let calorieCounter: HTMLElement;
  let budgetNumberInput: HTMLElement;
  let entryDropdown: HTMLElement;
  let addEntryButton: HTMLElement;
  let clearButton: HTMLElement;
  let output: HTMLElement;

  let isError = false;

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

      <fieldset id="breakfast">
        <legend>Breakfast</legend>
        <div class="input-container"></div>
      </fieldset>
      <fieldset id="lunch">
        <legend>Lunch</legend>
        <div class="input-container"></div>
      </fieldset>
      <fieldset id="dinner">
        <legend>Dinner</legend>
        <div class="input-container"></div>
      </fieldset>
      <fieldset id="snacks">
        <legend>Snacks</legend>
        <div class="input-container"></div>
      </fieldset>
      <fieldset id="exercise">
        <legend>Exercise</legend>
        <div class="input-container"></div>
      </fieldset>

      <div class="controls">
        <span>
          <label for="entry-dropdown">Add food or exercise:</label>
          <select bind:this={entryDropdown} id="entry-dropdown" name="options">
            <option value="breakfast" selected>Breakfast</option>
            <option value="lunch">Lunch</option>
            <option value="dinner">Dinner</option>
            <option value="snacks">Snacks</option>
            <option value="exercise">Exercise</option>
          </select>
          <button bind:this={addEntryButton} type="button" id="add-entry"
            >Add Entry</button
          >
        </span>
      </div>
      <div>
        <button type="submit">Calculate Remaining Calories</button>
        <button bind:this={clearButton} type="button" id="clear">Clear</button>
      </div>
    </form>
    <div bind:this={output} id="output" class="output hide"></div>
  </div>
</main>

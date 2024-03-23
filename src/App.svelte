<script lang="ts">
  import CalorieInput from "./components/CalorieInput.svelte";

  let budgetCalories: number;
  let clearButton: HTMLElement;
  let output: HTMLElement;

  type CalorieInputHandle = {
    id: number;
    name: string;
    input: CalorieInput | null;
    consumed: boolean;
  };
  const calorieInputHandles: CalorieInputHandle[] = [
    { id: 0, name: "breakfast", input: null, consumed: true },
    { id: 1, name: "lunch", input: null, consumed: true },
    { id: 2, name: "dinner", input: null, consumed: true },
    { id: 3, name: "snacks", input: null, consumed: true },
    { id: 4, name: "exercise", input: null, consumed: false },
  ];

  function calculateCalories() {
    const consumedCalories = calorieInputHandles
      .map((inputHandle) =>
        inputHandle.consumed && inputHandle.input
          ? inputHandle.input.getCaloriesSum()
          : 0
      )
      .reduce((sum, value) => sum + value);
    const burntCalories = calorieInputHandles
      .map((inputHandle) =>
        !inputHandle.consumed && inputHandle.input
          ? inputHandle.input.getCaloriesSum()
          : 0
      )
      .reduce((sum, value) => sum + value);
    const remainingCalories = budgetCalories - consumedCalories + burntCalories;

    const surplusOrDeficit = remainingCalories < 0 ? "Surplus" : "Deficit";

    output.innerHTML = `<span class="${surplusOrDeficit.toLowerCase()}">${Math.abs(
      remainingCalories
    )} Calorie ${surplusOrDeficit}</span>
  <hr>
  <p>${budgetCalories} Calories Budgeted</p>
  <p>${consumedCalories} Calories Consumed</p>
  <p>${burntCalories} Calories Burned</p>
  `;
    output.classList.remove("hide");
  }
</script>

<main>
  <h1>Calorie Counter</h1>
  <div class="container">
    <form on:submit|preventDefault={calculateCalories} id="calorie-counter">
      <label for="budget">Budget</label>
      <input
        bind:value={budgetCalories}
        type="number"
        min="0"
        id="budget"
        placeholder="Daily calorie budget"
        required
      />

      {#each calorieInputHandles as { id, name, input } (id)}
        <CalorieInput bind:this={input} {name} />
      {/each}

      <div>
        <button type="submit">Calculate Remaining Calories</button>
        <button bind:this={clearButton} type="button" id="clear">Clear</button>
      </div>
    </form>
    <div bind:this={output} id="output" class="output hide"></div>
  </div>
</main>

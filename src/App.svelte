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

  // function calculateCalories(e: Event) {
  //   e.preventDefault();
  //   isError = false;
  //   const breakfastNumberInputs = document.querySelectorAll(
  //     "#breakfast input[type=number]"
  //   );
  //   const lunchNumberInputs = document.querySelectorAll(
  //     "#lunch input[type=number]"
  //   );
  //   const dinnerNumberInputs = document.querySelectorAll(
  //     "#dinner input[type=number]"
  //   );
  //   const snacksNumberInputs = document.querySelectorAll(
  //     "#snacks input[type=number]"
  //   );
  //   const exerciseNumberInputs = document.querySelectorAll(
  //     "#exercise input[type=number]"
  //   );
  //   const breakfastCalories = getCaloriesFromInputs(breakfastNumberInputs);
  //   const lunchCalories = getCaloriesFromInputs(lunchNumberInputs);
  //   const dinnerCalories = getCaloriesFromInputs(dinnerNumberInputs);
  //   const snacksCalories = getCaloriesFromInputs(snacksNumberInputs);
  //   const exerciseCalories = getCaloriesFromInputs(exerciseNumberInputs);
  //   const budgetCalories = getCaloriesFromInputs([budgetNumberInput]);

  //   if (isError) {
  //     return;
  //   }

  //   const consumedCalories =
  //     breakfastCalories + lunchCalories + dinnerCalories + snacksCalories;
  //   const remainingCalories =
  //     budgetCalories - consumedCalories + exerciseCalories;
  //   const surplusOrDeficit = remainingCalories < 0 ? "Surplus" : "Deficit";

  //   output.innerHTML = `<span class="${surplusOrDeficit.toLowerCase()}">${Math.abs(
  //     remainingCalories
  //   )} Calorie ${surplusOrDeficit}</span>
  // <hr>
  // <p>${budgetCalories} Calories Budgeted</p>
  // <p>${consumedCalories} Calories Consumed</p>
  // <p>${exerciseCalories} Calories Burned</p>
  // `;
  //   output.classList.remove("hide");
  // }

  // calorieCounter.addEventListener("submit", calculateCalories);
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

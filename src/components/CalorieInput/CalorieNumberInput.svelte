<script lang="ts">
  export let name: string;
  export let order: number;

  let calories: number;

  export function getCalories() {
    return calories;
  }
</script>

<label for="${name}-${order}-calories">Entry {order} Calories</label>
<input
  bind:value={calories}
  type="number"
  min="0"
  placeholder="Calories"
  id="${name}-${order}-calories"
/>

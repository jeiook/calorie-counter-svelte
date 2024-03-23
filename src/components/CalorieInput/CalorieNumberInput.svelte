<script lang="ts">
  import { createEventDispatcher } from "svelte";

  export let name: string;
  export let order: number;

  let calories: number;
  const dispatch = createEventDispatcher();
</script>

<label for="${name}-${order}-calories">Entry {order} Calories</label>
<input
  bind:value={calories}
  on:input={() => dispatch("newInput", { calories })}
  type="number"
  min="0"
  placeholder="Calories"
  id="${name}-${order}-calories"
/>

<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { fade, fly } from 'svelte/transition';
  export let todo: string = "";
  export let id: number = 0;
  export let completed: boolean = false;
  export const dispatch = createEventDispatcher();
  const toggle = () => {
    dispatch("toggle", id);
  };
  const remove = () => {
    dispatch("remove", id);
  };


</script>

<div class="border p-4 flex justify-between bg-white rounded-lg shadow-lg my-2" in:fade out:fly={{x: 100}}>
  <div>
    <input type="checkbox" bind:checked={completed} on:change={toggle} />
    <span class="font-semibold text-2xl">{todo}</span>
  </div>
  <button class="bg-red-400 p-2 font-semibold rounded" on:click={remove}>Remove</button>
</div>

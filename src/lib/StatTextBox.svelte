<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  export let stat:string
  export let value:string

  const dispatch = createEventDispatcher();

  function update() {
    dispatch('update', { stat: stat, value: value });
  }
</script>

<div>
  <label>
    { stat }
    <input bind:value={value} on:blur={() => update()} />
  </label>
</div>

<style lang="sass">
input
  border: solid 1px #777
  border-radius: 4px
  padding: 4px
  margin: 4px
  line-height: 16px
  font-size: 14px
</style>

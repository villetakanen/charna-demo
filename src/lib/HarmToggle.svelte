<script lang="ts">
    import { createEventDispatcher } from 'svelte';
  
    export let stat:string
    export let value:string

    let permanent = parseInt(value) > 1
    let temporary = parseInt(value) > 0
    
    const dispatch = createEventDispatcher();
  
    function update() {
      dispatch('update', { stat: stat, value: value });
    }
  </script>
  
  <div>
    <input type="checkbox" checked={temporary}>
    <input type="checkbox" checked={permanent}>
    { stat }
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
  
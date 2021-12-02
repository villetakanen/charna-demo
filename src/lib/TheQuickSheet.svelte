<script lang="ts">
  import { CharacterSheet } from 'charna/lib'
import StatTextBox from './StatTextBox.svelte'
  let sheet = new CharacterSheet('A Demo of the Quick Character Sheet')
  sheet.model = 'thequickrpg'

  let backgrounds = sheet.getStat('backgrounds').value as string

  function stat(name: string, value: string) {
    sheet.setStat(name, value)
    sheet = sheet
  }

  function handleStatUpdate (event) {
    console.log(event.detail)
		stat(event.detail.stat, event.detail.value)
	}
</script>

<h1>{ sheet.id }</h1>

<div class="section">
  {#each sheet.statKeys() as statName }
    <StatTextBox
      value={'' + sheet.getStat(statName).value}
      stat={statName}
      on:update={handleStatUpdate}/>
  {/each}

  <hr>

  {#each sheet.statKeys() as statName }
    <p><strong>{ statName }</strong></p>
    <div>{@html sheet.getStat(statName).value }</div>
  {/each}
   
</div>

<style lang="sass">
h1
  font-size: 2em
  font-weight: bold
  margin-bottom: 0.5em
.section
  margin: 12px auto
</style>

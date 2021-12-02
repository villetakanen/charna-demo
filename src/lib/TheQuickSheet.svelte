<script lang="ts">
  import { CharacterSheet } from 'charna/lib'
import HarmToggle from './HarmToggle.svelte'
  import StatTextBox from './StatTextBox.svelte'
  let sheet = new CharacterSheet('A Demo of the Quick Character Sheet')
  sheet.model = 'thequickrpg'

  sheet.setStat('character_name', 'Thorbjörn Asmund')
  sheet.setStat('callsign', 'Thor!')
  sheet.setStat('concept', 'The Channel')
  sheet.setStat('backgrounds', 'Thor(!) is a 40 years old fisher and a boat mechanic from northern sweden')
  sheet.setStat('specialties', 'Thor races every man class')
  sheet.setStat('powers', 'Open the Gate')
  sheet.setStat('motivation', 'With Great Power')
  sheet.setStat('flaws', 'Weirdmagnet')
  sheet.setStat('Other Aspects', '-')
  sheet.setStat('Contacts', 'Siiri')
  sheet.setStat('harm_1',2)
  sheet.setStat('harm_2', 1)

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
    {#if sheet.getStat(statName).type === 'text'}
      <StatTextBox
        value={'' + sheet.getStat(statName).value}
        stat={statName}
        on:update={handleStatUpdate}/>
    {:else if sheet.getStat(statName).type === 'toggle' }
      <HarmToggle value={'' + sheet.getStat(statName).value} stat={statName} on:update={handleStatUpdate}/>
    {/if}
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

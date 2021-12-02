<script lang="ts">
  import { CharacterSheet } from 'charna/lib'
  let sheet = new CharacterSheet('A Demo of the Quik Character Sheet')
  sheet.model = 'thequickrpg'

  let backgrounds = sheet.getStat('backgrounds').value as string

  function stat(name: string, value: string) {
    sheet.setStat(name, value)
    sheet = sheet
  }
</script>

<section>
  { sheet.id } / 
  <div>{@html sheet.getStat('backgrounds').value }</div>
  <br>
  { sheet.statKeys() }
  <br>
  <input bind:value={ backgrounds } on:blur={() => stat('backgrounds', backgrounds)} />
</section>


<script setup lang="ts">
import Counter from './components/Counter.vue';
import Button from './components/Button.vue';
import ButtonWithField from './components/ButtonWithField.vue';
import KrarkCopies from './components/KrarkCopies.vue';
import SettingCheck from './components/SettingCheck.vue';
import Logs from './components/Logs.vue';

const logs = [
  {message: 'Flipped'},
  {message: 'My'},
  {message: 'Ass'},
  {message: 'Boye'},
]

</script>

<template>
  <header>
    <h1 class="u-full-width centered">Krarkulator</h1>
  </header>

  <main>
    <div class="container">
      <div class="row">
        <Button class="four columns" label="Cast" />
        <ButtonWithField class="four columns" label="Cast ritual" />
        <Button class="four columns" label="Next Turn" />
      </div>
    </div>
    <hr />
    <div class="container">

      <div class="row">
        <Counter class="three columns" title='Won flips' />
        <Counter class="three columns" title='Lost flips' />
        <Counter class="two columns" title='Storm counter' />
        <Counter class="two columns" title='Red mana' />
        <Counter class="two columns" title='Treasures' />
      </div>
    </div>
    <hr />
    <div class="container">
      <div class="row">
        <div class="four columns">
          <h2>Settings</h2>
          <div>
            <label for="krarkCopies">Krark copies</label>
            <input class="u-full-width" type="number" name="krarkCopies"/>
          </div>
          <h4>Flips</h4>
          <SettingCheck label="Krark's Thumb" />
          <SettingCheck label="Tavern Scoundrel" />
          <h4>Magecraft</h4>
          <SettingCheck label="Storm Kiln Artist" />
          <h4>Double Triggers</h4>
          <SettingCheck label="Veyran Voice of Duality" />
          <SettingCheck label="Harmonic Prodigy" />
        </div>

        <div class="eight columns">
          <h2>Logs</h2>
          <Logs v-model="logs"/>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.centered {
  text-align: center;
  vertical-align: middle;
}
</style>

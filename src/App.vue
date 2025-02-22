<script setup lang="ts">
import Counter from './components/Counter.vue'
import Button from './components/Button.vue'
import ButtonWithField from './components/ButtonWithField.vue'
import KrarkCopies from './components/KrarkCopies.vue'
import SettingCheck from './components/SettingCheck.vue'
import Logs from './components/Logs.vue'
import { ref } from 'vue'

const logs = ref([])

const krarkThumb = ref(false)
const tavernScoundrel = ref(false)
const stormKilnArtist = ref(false)
const veyran = ref(false)
const harmonicProdigy = ref(false)

const wonFlips = ref(0)
const lostFlips = ref(0)
const stormCount = ref(0)
const redMana = ref(0)
const treasures = ref(0)

function logAction(message) {
  logs.value.push(message)
}

function castSpell() {
}

function castRitual() {
}

function nextTurn() {
  stormCount.value = 0;
  redMana.value = 0;
  treasures.value = 0;
}

</script>

<template>
  <header>
    <h1 class="u-full-width centered">Krarkulator</h1>
  </header>

  <main>
    <div class="container">
      <div class="row">
        <Button @click="flipCoins" class="four columns" label="Cast" />
        <ButtonWithField class="four columns" label="Cast ritual" />
        <Button @click="nextTurn" class="four columns" label="Next Turn" />
      </div>
    </div>
    <hr />
    <div class="container">
      <h2 class="centered">Current Turn</h2>
      <div class="row">
        <Counter v-model="wonFlips" class="three columns" title="Won flips" />
        <Counter v-model="lostFlips" class="three columns" title="Lost flips" />
        <Counter v-model="stormCount" class="two columns" title="Storm counter" />
        <Counter v-model="redMana" class="two columns" title="Red mana" />
        <Counter v-model="treasures" class="two columns" title="Treasures" />
      </div>
    </div>
    <hr />
    <div class="container">
      <div class="row">
        <div class="four columns">
          <h2>Settings</h2>
          <div>
            <label for="krarkCopies">Krark copies</label>
            <input class="u-full-width" type="number" name="krarkCopies" />
          </div>
          <h4>Flips</h4>
          <SettingCheck
            @click="logAction({ message: 'Krark\'s Thumb toggled', value: krarkThumb })"
            v-model="krarkThumb"
            label="Krark's Thumb"
          />
          <SettingCheck
            @click="logAction({ message: 'Tavern Scoundrel toggled', value: tavernScoundrel })"
            v-model="tavernScoundrel"
            label="Tavern Scoundrel"
          />
          <h4>Magecraft</h4>
          <SettingCheck
            @click="logAction({ message: 'Storm-Kiln Artist toggled', value: stormKilnArtist })"
            v-model="stormKilnArtist"
            label="Storm Kiln Artist"
          />
          <h4>Double Triggers</h4>
          <SettingCheck
            @click="logAction({ message: 'Veyran, Voice of Duality toggled', value: veyran })"
            v-model="veyran"
            label="Veyran Voice of Duality"
          />
          <SettingCheck
            @click="logAction({ message: 'Harmonic Prodigy toggled', value: harmonicProdigy })"
            v-model="harmonicProdigy"
            label="Harmonic Prodigy"
          />
        </div>

        <div class="eight columns">
          <h2>Logs</h2>
          <Logs v-model="logs" />
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

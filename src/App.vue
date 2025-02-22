<script setup lang="ts">
import Counter from './components/Counter.vue'
import Button from './components/Button.vue'
import ButtonWithField from './components/ButtonWithField.vue'
import SettingCheck from './components/SettingCheck.vue'
import Logs from './components/Logs.vue'
import { ref } from 'vue'

const logs = ref([])

const krarkCopies = ref(0);

const krarkThumb = ref(false);
const tavernScoundrel = ref(false);
const stormKilnArtist = ref(false);
const birgi = ref(false);
const veyran = ref(false);
const harmonicProdigy = ref(false);

const wonFlips = ref(0);
const lostFlips = ref(0);
const stormCount = ref(0);
const redMana = ref(0);
const treasures = ref(0);

const ritualManaAmount = ref(0);

function logAction(message) {
  logs.value.push(message)
}

function flipCoin() {
  return Math.random() >= 0.5;
}

function flipCoins(triggerAmount) {
  const flippedCoins = Array(krarkCopies.value * triggerAmount).fill(0).map(flipCoin);
  if (krarkThumb.value) {
    console.log("WIP");
  }
  return {
    wonFlips: flippedCoins.filter((x) => x === true).length,
    lostFlips: flippedCoins.filter((x) => x === false).length,
    choiceFlips: 0,
  };
}

function getTriggerAmount() {
  console.log(1 + +veyran.value + +harmonicProdigy.value)
  return 1 + +veyran.value + +harmonicProdigy.value
}

function castValidations(triggerAmount) {
  if (birgi.value) {
    increaseRedMana(1*triggerAmount);
  }
  if (stormKilnArtist.value) {
    increaseTreasures(1*triggerAmount);
  }
}

function copyValidations(copyAmount, triggerAmount) {
  if (stormKilnArtist.value) {
    increaseTreasures(1*copyAmount*triggerAmount)
  }
}

function increaseRedMana(x) {
  redMana.value = redMana.value + x;
}

function increaseTreasures(x) {
  treasures.value = treasures.value + x;
}

function increaseStormCount() {
  stormCount.value++;
}

//Actions
function castRitual() {
  logAction({
    message: `Casting a ritual of ${ritualManaAmount.value} mana...`,
    ritualAmount: ritualManaAmount.value,
  });
  const triggerAmount = getTriggerAmount();
  increaseStormCount()
  castValidations(triggerAmount)
  const result = flipCoins(triggerAmount);
  wonFlips.value = result.wonFlips;
  lostFlips.value = result.lostFlips;
  copyValidations(result.wonFlips, triggerAmount);
  increaseRedMana(result.wonFlips * ritualManaAmount.value)
  logAction({message: `The cast cointains ${wonFlips.value} won flips and ${lostFlips.value} lost flips`});
}

function castSpell() {
  logAction({
    message: `Casting a spell...`,
    ritualAmount: ritualManaAmount.value,
  });

  const triggerAmount = getTriggerAmount();
  increaseStormCount();
  castValidations(triggerAmount)
  const result = flipCoins(triggerAmount);
  wonFlips.value = result.wonFlips;
  lostFlips.value = result.lostFlips;
  copyValidations(result.wonFlips, triggerAmount);
  logAction({message: `The cast cointains ${wonFlips.value} won flips and ${lostFlips.value} lost flips`});
}

function nextTurn() {
  stormCount.value = 0;
  redMana.value = 0;
  treasures.value = 0;
  logAction({
    message: 'Going into next turn'
  });
}

</script>

<template>
  <header>
    <h1 class="u-full-width centered">Krarkulator</h1>
  </header>

  <main>
    <div class="container">
      <div class="row">
        <Button @click="castSpell" class="four columns" label="Cast" />
        <ButtonWithField @on-cast="castRitual" v-model='ritualManaAmount' class="four columns" label="Cast ritual" />
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
            <input class="u-full-width" type="number" v-model="krarkCopies" />
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
          <SettingCheck
            @click="logAction({ message: 'Birgi, God of Storytelling toggled', value: birgi })"
            v-model="birgi"
            label="Birgi, God of Storytelling"
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

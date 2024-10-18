<script setup lang="ts">
import { ref } from 'vue';

const awesome = ref(true);
const jegy = ref(5);
</script>

<template>
  <q-page class="column flex-center">
    <h2>A v-if és v-else direktívák</h2>
    <!-- v-if vue direktíva az elem megjelenését vezérli a megadott feltétel kiértékelése után -->
    <!-- Az elem fizikailag nem kerül a renderelt dokumentumba, nemcsak a display tulajdonsága van beállítva none-ra -->
    <!-- A v-else a "hamis" ágat határozza meg, elhagyható, de közvetlenül a v-if utáni elemben kell, hogy legyen.-->
    <q-banner v-if="awesome" class="bg-warning text-black full-width text-center">Vue is awesome!</q-banner>
    <q-banner v-else class="bg-primary text-white full-width text-center">Oh no 😢</q-banner>
    <q-btn class="q-mt-xl" color="primary" glossy label="Toggle" no-caps @click="awesome = !awesome" />

    <h2>A v-else-if direktíva használata</h2>
    <q-input v-model.number="jegy" clearable label="Jegy" outlined type="number" />
    <q-banner v-if="jegy == 5" class="bg-primary text-white full-width text-center">Jeles</q-banner>
    <q-banner v-else-if="jegy == 4" class="bg-primary text-white full-width text-center">Jó</q-banner>
    <q-banner v-else-if="jegy == 3" class="bg-primary text-white full-width text-center">Közepes </q-banner>
    <q-banner v-else-if="jegy == 2" class="bg-primary text-white full-width text-center">Elégséges</q-banner>
    <q-banner v-else-if="jegy == 1" class="bg-primary text-white full-width text-center">Elégtelen</q-banner>
    <q-banner v-else class="bg-primary text-white full-width text-center">Nem osztályzat!</q-banner>

    <!-- v-show vue direktíva az elem megjelenését vezérli a megadott feltétel kiértékelése után -->
    <!-- Az elem fizikailag a renderelt dokumentumban marad, csak a display tulajdonsága van beállítva none-ra -->
    <h2>A v-show direktíva</h2>
    <q-banner v-show="awesome" class="bg-warning text-black full-width text-center"
      >A display tulajdonság állítása, vizsgáld meg F12-vel!</q-banner
    >

    <!-- v-if on <template> -->
    <!-- https://vuejs.org/guide/essentials/conditional.html#v-if-on-template -->
  </q-page>
</template>

<style lang="scss" scoped></style>

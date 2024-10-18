<!-- 04. - Bindings -->
<!-- Vue.js Guide: https://vuejs.org/guide/essentials/class-and-style.html -->

<script setup lang="ts">
import { ref, reactive } from 'vue';

const dynamicId = ref(undefined);
const id = ref('myDinamicId');

const activeColor = ref('red');

const styleObject = reactive({
  color: 'blue',
  fontSize: '80px',
  backgroundColor: 'yellow', // CSS tulajdonság camelCase-ben is megadható snake-case helyett
  // vagy:
  // 'background-color': 'yellow',
  //  background-color helyett: backgroundColor
});

const objectOfAttrs = reactive({
  id: 'container',
  class: 'q-my-md',
  style: 'background-color:green',
});

const isBold = ref(false);
const isActive = ref(false);
const attribNeve = ref('no-caps');

function toggleBold() {
  isBold.value = !isBold.value;
}

function toggleAttrib() {
  if (attribNeve.value === 'no-caps') {
    attribNeve.value = 'rounded';
  } else {
    attribNeve.value = 'no-caps';
  }
}

function toggleActive() {
  isActive.value = !isActive.value;
}
</script>

<template>
  <!-- Bindings: Egyirányú adatkötés -->
  <!-- Vue.js direktívája a "v-bind:", rövidítése ":" -->
  <q-page>
    <!-- Attribute Bindings -->
    <!-- If dynamicId value is undefined, then the attribute will be removed from the rendered element. -->
    <p :id="dynamicId">Bekezdés dinamikus id-val (F12-vel keresd meg az azonosítóját!)</p>
    <q-input v-model="dynamicId" clearable label="Add meg a paragrafus azonosítóját!" outlined />

    <!-- Same-name Shorthand -->
    <!-- Ha a TS/JS változó azonosítója eggyezik az attribútum azonosítójával, akkor röviden: -->
    <p :id>Ennek a paragrafusnak az id-ja: 'myDinamicId'</p>

    <!-- Style bindings -->
    <!-- <h2 v-bind:style="{ color: activeColor }">Style binding</h2> -->
    <h2 :style="{ color: activeColor }">Style binding</h2>
    <q-input v-model="activeColor" clearable label="Szín" outlined />
    <h2 :style="styleObject">Style bindings with object</h2>

    <!-- Class bindings -->
    <h2 :class="{ bold: isBold }">Class binding - is bold?</h2>
    <q-btn color="primary" glossy label="Bold/Normal" no-caps @click="toggleBold()" />

    <!-- Példa attributes binding-ra Quasar elemekkel, boolean típusú attribútummal -->
    <!-- A példában az előző feladat isBold reaktív változóját használjuk -->
    <q-btn color="primary" :disable="isBold" glossy label="disable true/false" no-caps />
    <q-banner :dense="isBold">Ez a banner szövege (dense true/false)</q-banner>

    <!-- Példa Object of attributes binding-ra -->
    <!-- Ilyenkor a v-bind rövidítése nem használható -->
    <q-banner v-bind="objectOfAttrs">Object of attributes binding</q-banner>

    <!-- Péda dinamikus attributumokra -->
    <q-btn :[attribNeve]="isActive">Péda dinamikus attribútumra</q-btn>
    <div>
      <q-btn
        color="primary"
        glossy
        :label="attribNeve == 'no-caps' ? 'no-caps' : 'rounded'"
        no-caps
        @click="toggleAttrib()"
      />
      <q-btn color="primary" glossy :label="`isActive = ${isActive}`" no-caps @click="toggleActive()" />
    </div>

    <!-- További lehetőségek a binding-ra (pl.: Binding to Arrays) -->
    <!-- https://vuejs.org/guide/essentials/class-and-style.html -->
  </q-page>
</template>

<style lang="scss" scoped>
.bold {
  font-weight: bold;
  // font-size: 40px;
}
.q-banner {
  font-size: 20px;
  color: red;
  width: 300px;
  background-color: lightblue;
}

#myId {
  color: blue;
}
</style>

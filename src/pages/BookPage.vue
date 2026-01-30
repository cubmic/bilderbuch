<template>
  <q-page
    class="flex justify-center q-pa-md"
    :style="`background-color:${pages[actualPage - 1].color}`"
  >

    <!-- menu -->
    <div class="row q-col-gutter-md fit justify-between">
      <div class="col-auto">
        <q-btn
          v-if="actualPage > 1"
          color="primary"
          icon="keyboard_arrow_left"
          label="zurück"
          :to="`/page/${actualPage - 1}`"
          style="width:130px"
        />
      </div>
      <div class="col-auto">
        <q-btn
          v-if="actualPage < pages.length"
          color="primary"
          icon-right="keyboard_arrow_right"
          label="weiter"
          :to="`/page/${actualPage + 1}`"
          style="width:130px"
        />
      </div>
    </div>

    <h1>{{ pages[actualPage - 1].title }}</h1>
  </q-page>
</template>

<script setup>
import { computed } from 'vue';
import { useRoute } from 'vue-router'
const route = useRoute()

const actualPage = computed(() => {
  return parseInt(route.params.page)
})
const pages = [
  {
    title: 'Seite 1',
    color: 'rgb(36, 149, 153)'
  },
  {
    title: 'Seite 2',
    color: 'rgb(167, 109, 203)'
  },
  {
    title: 'Seite 3',
    color: 'rgb(203, 183, 109)'
  }
]
</script>

<template>
  <q-page class="q-mt-md" :style="`background-color:${pages[actualPage - 1].color}`">
    <!-- menu -->
    <div class="row q-col-gutter-md fit justify-between">
      <div class="col-auto">
        <q-btn
          v-if="actualPage > 1"
          color="primary"
          icon="keyboard_arrow_left"
          label="zurück"
          :to="`/page/${actualPage - 1}`"
          style="width: 130px"
        />
      </div>
      <div class="col-auto">
        <q-btn
          v-if="actualPage < pages.length"
          color="primary"
          icon-right="keyboard_arrow_right"
          label="weiter"
          :to="`/page/${actualPage + 1}`"
          style="width: 130px"
        />
      </div>
    </div>

    <h1>{{ page.title }}</h1>

    <div class="container" ref="containerRef">
      <div
        v-for="element in page.elements"
        :key="element.id"
        :style="{
          position: 'absolute',
          zIndex: element.zIndex,
          top: `${element.top}px`,
          left: `${left * element.speed}px`,
        }"
      >
        <img :src="element.img" />
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute()

const containerRef = ref()
const left = ref(0)

const actualPage = computed(() => {
  return parseInt(route.params.page)
})

const page = computed(() => {
  return pages[actualPage.value - 1]
})

const pages = [
  {
    title: 'Seite 1',
    color: 'rgb(36, 149, 153)',
    elements: [
      {
        id: 1,
        speed: 0,
        zIndex: 1,
        top: 0,
        img: 'src/assets/berg.png',
      },
      {
        id: 2,
        speed: 0.5,
        zIndex: 2,
        top: 50,
        img: 'src/assets/hirsch.png',
      },
    ],
  },
  {
    title: 'Seite 2',
    color: 'rgb(167, 109, 203)',
  },
  {
    title: 'Seite 3',
    color: 'rgb(203, 183, 109)',
  },
]

function scroll(event) {
  left.value = event.target.scrollLeft
}

onMounted(() => {
  containerRef.value.addEventListener('scroll', scroll)
})
</script>

<style lang="css">
h1 {
  margin: 0;
  padding: 0;
}
.container {
  position: relative;
  width: 100vw;
  height: 400px;
  overflow-x: scroll;
  overflow-y: hidden;
}
</style>

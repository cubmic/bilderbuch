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
        v-for="(element, index) in page.elements"
        :key="index"
        class="animate__animated"
        :class="
          element.effects
            ?.filter((o) => o.left < left)
            ?.map((o) => o.effect)
            .join(' ') || ''
        "
        :style="{
          position: 'absolute',
          zIndex: element.zIndex,
          top: `${element.top}px`,
          left: `${left * element.speed + element.left}px`
        }"
      >
        <img
          :src="element.img"
          :style="{
            width: `${element.width}px`
          }"
        />
      </div>
    </div>
    <div class="textblock">
      {{ text }}
    </div>
  </q-page>
</template>

<script setup>
import 'animate.css'
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

const text = computed(() => {
  return (
    page.value.texts?.find((o) => {
      return o.left > left.value
    })?.text || ''
  )
})

const pages = [
  {
    title: 'Seite 1',
    color: 'rgb(36, 149, 153)',
    texts: [
      {
        left: 200,
        text: `Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat.`,
      },
      {
        left: 600,
        text: `Monsen`,
      },
    ],
    elements: [
      {
        speed: 0,
        zIndex: 0,
        left: 170,
        top: 140,
        img: 'src/assets/Schneelandschaft.png',
        width: 300
      },
      {
        speed: 0,
        zIndex: 2,
        left: 715,
        top: 50,
        img: 'src/assets/Lampe.png',
        width: 100
      },
      {
        speed: 0,
        zIndex: 1,
        left: 60,
        top: 50,
        img: 'src/assets/Katze_am_Fenster.png',
        width: 700
      },
      {
        speed: 0,
        zIndex: 1,
        left: 715,
        top: 50,
        img: 'src/assets/Katzengesicht.png',
        width: 500
      },
      {
        speed: 0,
        zIndex: 0,
        left: 1150,
        top: 50,
        img: 'src/assets/Schneelandschaft.png',
        width: 1000
      },
      {
        speed: 0.25,
        zIndex: 2,
        left: 1200,
        top: -75,
        img: 'src/assets/baum.png',
        width: 1000,
        effects: [
          {
            left: 800,
            effect: 'animate__flipInY',
          },
          {
            left: 1200,
            effect: 'animate__hinge',
          },
        ],
      },
    ],
  },
  {
    title: 'Seite 2',
    color: 'rgb(167, 109, 203)',
    elements: [
      {
        speed: 0,
        zIndex: 1,
        left: 1050,
        top: 50,
        img: 'src/assets/Baer1.png',
        width: 100
      },
      {
        speed: 0,
        zIndex: 1,
        left: 2020,
        top: 50,
        img: 'src/assets/Baer2.png',
        width: 100
      },
      {
        speed: 0,
        zIndex: 1,
        left: 1150,
        top: 0,
        img: 'src/assets/Fuchs1.png',
        width: 70
      },
      {
        speed: 0,
        zIndex: 1,
        left: 2120,
        top: 0,
        img: 'src/assets/Fuchs2.png',
        width: 70
      },
      {
        speed: 0,
        zIndex: 0,
        left: 640,
        top: 0,
        img: 'src/assets/Curlingbahn.png',
        width: 1000
      },
      {
        speed: 0,
        zIndex: 0,
        left: 1600,
        top: 0,
        img: 'src/assets/Curlingbahn.png',
        width: 1000
      },
      {
        speed: 0,
        zIndex: 0,
        left: 730,
        top: 90,
        img: 'src/assets/Katze4.png',
        width: 150
      },
      {
        speed: 0,
        zIndex: 1,
        left: 1200,
        top: 50,
        img: 'src/assets/Hirsch1.png',
        width: 100
      },
      {
        speed: 0,
        zIndex: 1,
        left: 2170,
        top: 50,
        img: 'src/assets/Hirsch2.png',
        width: 100
      },
      {
        speed: 0,
        zIndex: 1,
        left: 1100,
        top: 200,
        img: 'src/assets/Curlingstein1.png',
        width: 50
      },
      {
        speed: 0,
        zIndex: 1,
        left: 1350,
        top: 250,
        img: 'src/assets/Curlingstein2.png',
        width: 50
      },
      {
        speed: 0,
        zIndex: 3,
        left: 1450,
        top: 50,
        img: 'src/assets/Katze3.png',
        width: 500
      },
    ],
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
.textblock {
  margin: 20px;
  width: 400px;
}
</style>

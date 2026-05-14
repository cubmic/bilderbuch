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
          left: `${left * element.speed + element.left}px`,
          transform: element.flipX ? 'scaleX(-1)' : '',
          filter: element.shadow ? `drop-shadow(${left * element.speed / 2}px 30px 10px rgba(0,0,0,0.5))` : '',
          borderRadius: element.round ? '50%' : '',
          overflow: element.round ? 'hidden' : ''
        }"
      >
        <img
          :src="element.img"
          :style="{
            width: `${element.width}px`
          }"
        />
      </div>
      <div :style="`position:absolute; left:${Math.max(...page.elements.map(o => o.left + o.width)) + 600}px;`">&nbsp;</div>
    </div>
    <div class="textblock">
      {{ text }}
    </div>
  </q-page>
</template>

<script setup>
import 'animate.css'
import { ref, watch, computed, onMounted } from 'vue'
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

watch(
  () => actualPage.value,
  () => {
    containerRef.value.scrollLeft = 0
  }
)

const pages = [
  {
    title: "Minka's Endeckung",
    color: 'rgb(36, 149, 153)',
    texts: [
      {
        left: 200,
        text: `Minka lebte in einer Welt, in der Tiere sprechen, spielen und zusammenleben wie Menschen. Sie war eine kleine, weiße Katze mit weichem Fell und leuchtend blauen Augen.`,
      },
      {
        left: 600,
        text: `Am liebsten saß sie am Fenster ihres gemütlichen Hauses. Von dort aus konnte sie die verschneite Landschaft sehen.`,
      },
      {
        left: 1000,
        text: `An diesem Tag fielen dicke Schneeflocken vom Himmel. Sie tanzten in der Luft, drehten sich und glitzerten im Licht. Minka beobachtete jede einzelne ganz genau.`,
      },
      {
        left: 1500,
        text: `„Wie schön der Winter ist“, murmelte sie leise und legte ihre Pfoten ans Fenster.`,
      },
      {
        left: 2000,
        text: `Doch plötzlich entdeckte sie in der Ferne etwas Neues: Auf einer großen Eisfläche bewegten sich Tiere hin und her. Neugierig sprang Minka vom Fenster und lief hinaus in den Schnee.`,
      },
    ],
    elements: [
      {
        speed: 0.15,
        zIndex: 0,
        left: 570,
        top: 65,
        img: 'images/Schneelandschaft.png',
        width: 350,
        flipX: true
      },
      {
        speed: 0.15,
        zIndex: 0,
        left: 720,
        top: 65,
        img: 'images/Schneelandschaft.png',
        width: 350
      },
      {
        speed: -0.2,
        zIndex: 2,
        left: 1000,
        top: 60,
        img: 'images/Lampe.png',
        width: 300,
        shadow: true
      },
      {
        speed: 0,
        zIndex: 1,
        left: 500,
        top: -100,
        img: 'images/Katze_am_Fenster.png',
        width: 900
      },
      {
        speed: 0,
        zIndex: 1,
        left: 1350,
        top: 150,
        img: 'images/ornamente.png',
        width: 300
      },
      {
        speed: 0,
        zIndex: 1,
        left: 1750,
        top: 55,
        img: 'images/Katzengesicht.png',
        width: 300
      },
      {
        speed: 0,
        zIndex: 1,
        left: 2150,
        top: 150,
        img: 'images/ornamente.png',
        width: 300
      },
      {
        speed: 0,
        zIndex: 1,
        left: 2350,
        top: 0,
        img: 'images/Schneelandschaft.png',
        width: 1100,
        shadow: true
      },
      {
        speed: 0.1,
        zIndex: 0,
        left: 2400,
        top: -100,
        img: 'images/Berge3.png',
        width: 800
      },
    ],
  },
  {
    title: 'Das Spiel auf dem Eis',
    color: 'rgb(167, 109, 203)',
    texts: [
      {
        left: 200,
        text: `Als Minka näher kam, sah sie, was die Tiere taten. Sie spielten Curling auf einem gefrorenen See. Große Steine glitten über das Eis, während andere Tiere eifrig davor herfegten.`,
      },
      {
        left: 600,
        text: `Es sah spannend aus!`,
      },
      {
        left: 1000,
        text: `Minka setzte sich an den Rand und beobachtete das Spiel. Schließlich fasste sie sich ein Herz und rief: „Darf ich auch mitspielen?“`,
      },
      {
        left: 1500,
        text: `Doch kaum hatte sie das gesagt, begannen einige Tiere zu lachen.`,
      },
      {
        left: 2000,
        text: `„Du bist viel zu klein!“ rief ein Elch. „Der Stein ist schwerer als du!“ brummte ein Bär.`,
      },
      {
        left: 2500,
        text: `Minka senkte den Kopf. Ihr Herz fühlte sich schwer an. Aber tief in ihr drin wuchs ein Gedanke: Ich werde es ihnen zeigen.`,
      },
    ],
    elements: [
      {
        speed: 0.05,
        zIndex: 1,
        left: 700,
        top: 50,
        img: 'images/Baer1.png',
        width: 100
      },
      {
        speed: 0.05,
        zIndex: 1,
        left: 830,
        top: 20,
        img: 'images/Fuchs1.png',
        width: 70
      },
      {
        speed: 0,
        zIndex: 0,
        left: 360,
        top: -200,
        img: 'images/Curlingbahn.png',
        width: 1000
      },
      {
        speed: 0.05,
        zIndex: 0,
        left: 430,
        top: 90,
        img: 'images/Katze4.png',
        width: 200
      },
      {
        speed: 0.05,
        zIndex: 1,
        left: 890,
        top: 50,
        img: 'images/Hirsch1.png',
        width: 100
      },
      {
        speed: 0,
        zIndex: 1,
        left: 800,
        top: 200,
        img: 'images/Curlingstein1.png',
        width: 50
      },
      {
        speed: 0,
        zIndex: 1,
        left: 970,
        top: 190,
        img: 'images/Curlingstein2.png',
        width: 50
      },
      {
        speed: 0,
        zIndex: 1,
        left: 1030,
        top: 230,
        img: 'images/Curlingstein3.png',
        width: 50
      },
      {
        speed: 0,
        zIndex: 1,
        left: 870,
        top: 180,
        img: 'images/Curlingstein4.png',
        width: 50
      },
      {
        speed: 0,
        zIndex: 1,
        left: 1300,
        top: 150,
        img: 'images/ornamente.png',
        width: 300
      },
      {
        speed: 0.1,
        zIndex: 2,
        left: 1490,
        top: -50,
        img: 'images/Hirsch1.png',
        width: 500
      },
      {
        speed: 0.1,
        zIndex: 1,
        left: 1600,
        top: -200,
        img: 'images/Baer1.png',
        width: 700
      },
      {
        speed: 0.02,
        zIndex: 3,
        left: 1650,
        top: 50,
        img: 'images/Fuchs1.png',
        width: 500
      },
      {
        speed: 0,
        zIndex: 1,
        left: 2450,
        top: 150,
        img: 'images/ornamente.png',
        width: 300
      },
      {
        speed: 0.1,
        zIndex: 3,
        left: 2300,
        top: -290,
        img: 'images/Katze3.png',
        width: 870,
      },
      {
        speed: 0,
        zIndex: 1,
        left: 3200,
        top: 150,
        img: 'images/ornamente.png',
        width: 300
      },
      {
        speed: 0.1,
        zIndex: 2,
        left: 3200,
        top: -50,
        img: 'images/Hirsch2.png',
        width: 500,
        effects: [
          {
            left: 2720,
            effect: 'animate__shakeY',
          },
        ],
      },
      {
        speed: 0.1,
        zIndex: 1,
        left: 3300,
        top: -200,
        img: 'images/Baer2.png',
        width: 700,
        effects: [
          {
            left: 2700,
            effect: 'animate__shakeY',
          },
        ],
      },
      {
        speed: 0.02,
        zIndex: 3,
        left: 3600,
        top: 50,
        img: 'images/Fuchs2.png',
        width: 500,
        effects: [
          {
            left: 2710,
            effect: 'animate__shakeY',
          },
        ],
      },
    ],
  },
  {
    title: 'Heimliches Training',
    color: 'rgb(203, 183, 109)',
    elements: []
  },
  {
    title: 'Der große Versuch',
    color: 'rgb(118, 218, 134)',
    elements: []
  },
  {
    title: 'Minka zeigt, was sie kann',
    color: 'rgb(209, 80, 181)',
    elements: []
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
/* Hide scrollbar for Chrome, Safari and Opera */
.container::-webkit-scrollbar {
  display: none;
}

/* Hide scrollbar for IE, Edge and Firefox */
.container {
  -ms-overflow-style: none;  /* IE and Edge */
  scrollbar-width: none;  /* Firefox */
}
.textblock {
  margin: 20px auto;
  width: 400px;
  text-align: center;
  font-size: 20px;
}
</style>

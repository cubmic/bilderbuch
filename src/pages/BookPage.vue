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
          [
            element.effects
              ?.filter((o) => o.initial)
              ?.map((o) => o.initial)
              .join(' ') || '',
            element.effects
              ?.filter((o) => o.effect && o.left < left)
              ?.map((o) => o.effect)
              .join(' ') || ''
          ].join(' ')
        "
        :style="{
          position: 'absolute',
          zIndex: element.zIndex,
          top: `${element.top}px`,
          left: `${left * element.speed + element.left}px`,
          transform: element.flipX ? 'scaleX(-1)' : '',
          filter: element.shadow ? `drop-shadow(${left * element.speed / 2}px 30px 10px rgba(0,0,0,0.5))` : '',
          borderRadius: element.round ? '50%' : '',
          overflow: element.round ? 'hidden' : '',
          backgroundColor: element.backgroundColor || '',
          width: element.width ? `${element.width}px` : '',
          height: element.height ? `${element.height}px` : ''
        }"
      >
        <img
          v-if="element.img"
          :src="element.img"
          :style="{
            width: `${element.width}px`
          }"
        />
      </div>
      <div :style="`position:absolute; left:${Math.max(...page.elements.map(o => o.left + o.width)) + 600}px;`">&nbsp;</div>
    </div>
    <p class="textblock">
      {{ text }}
    </p>
  </q-page>
</template>

<script setup>
import 'animate.css'
import { ref, watch, computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute()

const containerRef = ref()
const left = ref(0)
const pageCenterX = ref(0)

const actualPage = computed(() => {
  return parseInt(route.params.page)
})

const page = computed(() => {
  return pages.value[actualPage.value - 1]
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

const pages = computed(() => {
  return [
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
          zIndex: 3,
          left: 1350,
          top: 150,
          img: 'images/ornament.png',
          width: 300
        },
        {
          speed: 0,
          zIndex: 0,
          left: 1650,
          top: 80,
          width: 400,
          height: 245,
          backgroundColor: 'rgb(242, 240, 217)'
        },
        {
          speed: 0,
          zIndex: 1,
          left: 1750,
          top: 140,
          img: 'images/Katzengesicht.png',
          width: 200
        },
        {
          speed: 0.05,
          zIndex: 2,
          left: 1925,
          top: 0,
          width: 150,
          height: 400,
          backgroundColor: 'rgb(36, 149, 153)'
        },
        {
          speed: 0.05,
          zIndex: 2,
          left: 1555,
          top: 0,
          width: 150,
          height: 400,
          backgroundColor: 'rgb(36, 149, 153)'
        },
        {
          speed: 0.05,
          zIndex: 3,
          left: 1550,
          top: -20,
          img: 'images/fenster.png',
          width: 600
        },
        {
          speed: 0,
          zIndex: 1,
          left: 2150,
          top: 150,
          img: 'images/ornament.png',
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
          img: 'images/ornament.png',
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
          img: 'images/ornament.png',
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
          img: 'images/ornament.png',
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
              left: 3320,
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
              left: 3300,
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
              left: 3310,
              effect: 'animate__shakeY',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 1,
          left: 4300,
          top: 150,
          img: 'images/ornament.png',
          width: 300
        },
        {
          speed: 0,
          zIndex: 3,
          left: 4500,
          top: -290,
          img: 'images/Katze3.png',
          width: 870,
        },
      ],
    },
    {
      title: 'Heimliches Training',
      color: 'rgb(203, 183, 109)',
      texts: [
        {
          left: 200,
          text: `In den folgenden Nächten kam Minka heimlich zurück zum See. Der Mond schien auf das Eis und ließ es silbern glänzen.`,
        },
        {
          left: 600,
          text: `Ganz allein begann sie zu üben.`,
        },
        {
          left: 1000,
          text: `Sie schob kleine Steine über das Eis, übte das Gleichgewicht und versuchte zu verstehen, wie sich die Steine bewegen.`,
        },
        {
          left: 1500,
          text: `Manchmal rutschte sie aus und fiel hin. Manchmal lief alles schief. Doch Minka gab nicht auf.`,
        },
        {
          left: 2000,
          text: `Mit jeder Nacht wurde sie besser. Ihre Bewegungen wurden ruhiger, ihr Blick sicherer.`,
        },
        {
          left: 2500,
          text: `Und jedes Mal dachte sie: Ich schaffe das.`,
        },
      ],
      elements: [
      {
          speed: 0,
          zIndex: 1,
          left: 360,
          top: -200,
          img: 'images/Curlingbahn.png',
          width: 1000,
          effects: [
            {
              left: 10,
              initial: 'animate__fadeIn-initial',
              effect: 'animate__fadeIn',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 2,
          left: 1550,
          top: -80,
          img: 'images/Bäume.png',
          width: 700,
          effects: [
            {
              left: 650,
              initial: 'animate__scaleTopIn-initial',
              effect: 'animate__scaleTopIn',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 1,
          left: 1500,
          top: 200,
          img: 'images/curlingbahn2.png',
          width: 800
        },
        {
          speed: 0,
          zIndex: 3,
          left: 1600,
          top: 200,
          img: 'images/Katze5.png',
          width: 300,
          effects: [
            {
              left: 1000,
              effect: 'animate__slideRightABit',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 2,
          left: 2550,
          top: -80,
          img: 'images/Bäume.png',
          width: 700,
          effects: [
            {
              left: 1650,
              initial: 'animate__scaleTopIn-initial',
              effect: 'animate__scaleTopIn',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 1,
          left: 2500,
          top: 200,
          img: 'images/curlingbahn2.png',
          width: 800
        },
        {
          speed: 0,
          zIndex: 3,
          left: 2600,
          top: 150,
          img: 'images/Katze1.png',
          width: 220
        },
        {
          speed: 0,
          zIndex: 3,
          left: 2710,
          top: 285,
          img: 'images/Curlingstein4.png',
          width: 90,
          effects: [
            {
              left: 2140,
              effect: 'animate__slideRightABit100',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 2,
          left: 3550,
          top: -80,
          img: 'images/Bäume.png',
          width: 700,
          effects: [
            {
              left: 2650,
              initial: 'animate__scaleTopIn-initial',
              effect: 'animate__scaleTopIn',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 1,
          left: 3500,
          top: 200,
          img: 'images/curlingbahn2.png',
          width: 800
        },
        {
          speed: 0,
          zIndex: 3,
          left: 3600,
          top: 150,
          img: 'images/Katze1.png',
          width: 220
        },
        {
          speed: 0,
          zIndex: 3,
          left: 3710,
          top: 285,
          img: 'images/Curlingstein1.png',
          width: 90,
          effects: [
            {
              left: 3140,
              effect: 'animate__slideRightABit300',
            },
          ],
        },
      
      ]
    },
    {
      title: 'Der große Versuch',
      color: 'rgb(118, 218, 134)',
      texts: [
        {
          left: 200,
          text: `Eines Tages fehlte einem Team beim Curling ein Spieler.`,
        },
        {
          left: 600,
          text: `„Wir brauchen jemanden!“, rief ein Tier.`,
        },
        {
          left: 1000,
          text: `Minka trat vorsichtig näher. „Ich könnte helfen…“`,
        },
        {
          left: 1500,
          text: `Die anderen zögerten, doch schließlich nickten sie.`,
        },
        {
          left: 2000,
          text: `Das Spiel begann. Minka war nervös, aber sie erinnerte sich an ihr Training.`,
        },
        {
          left: 2500,
          text: `Dann kam der entscheidende Moment: der letzte Stein. Alles hing von ihr ab.`,
        },
        {
          left: 2800,
          text: `Minka atmete tief durch, konzentrierte sich und schob den Stein mit ruhiger Pfote über das Eis.`,
        },
        {
          left: 3200,
          text: `Alle schauten gespannt zu. Der Stein glitt, drehte sich leicht… und kam genau im Ziel zum Liegen.`,
        },
      ],
      elements: [
        {
          speed: 0,
          zIndex: 1,
          left: 360,
          top: -200,
          img: 'images/Curlingbahn.png',
          width: 1000
        },
        {
          speed: 0,
          zIndex: 3,
          left: 450,
          top: 50,
          img: 'images/Katze4.png',
          width: 200
        },
        {
          speed: 0,
          zIndex: 2,
          left: 900,
          top: 90,
          img: 'images/Fuchs1.png',
          width: 100
        },
        {
          speed: 0,
          zIndex: 3,
          left: 950,
          top: 120,
          img: 'images/Fuchs1.png',
          width: 100
        },
        {
          speed: 0,
          zIndex: 2,
          left: 700,
          top: 65,
          img: 'images/Fuchs1.png',
          width: 100
        },
        {
          speed: 0,
          zIndex: 2,
          left: 700,
          top: 95,
          img: 'images/Baer1.png',
          width: 100
        },
        {
          speed: 0,
          zIndex: 2,
          left: 650,
          top: 75,
          img: 'images/Baer1.png',
          width: 100
        },
        {
          speed: 0,
          zIndex: 2,
          left: 950,
          top: 80,
          img: 'images/Hirsch1.png',
          width: 100
        },
        {
          speed: 0,
          zIndex: 2,
          left: 750,
          top: 80,
          img: 'images/Hirsch1.png',
          width: 100
        },
        {
          speed: 0,
          zIndex: 2,
          left: 1700,
          top: 100,
          img: 'images/Fuchs1.png',
          width: 250
        },
        {
          speed: 0,
          zIndex: 2,
          left: 1950,
          top: 100,
          img: 'images/Fuchs1.png',
          width: 250
        },
        {
          speed: 0,
          zIndex: 2,
          left: 1800,
          top: 100,
          img: 'images/Hirsch1.png',
          width: 250
        },
        {
          speed: 0,
          zIndex: 3,
          left: 2500,
          top: 50,
          img: 'images/Katze3.png',
          width: 400
        },
        {
          speed: 0,
          zIndex: 1,
          left: 3000,
          top: 200,
          img: 'images/curlingbahn2.png',
          width: 800
        },
        {
          speed: 0,
          zIndex: 2,
          left: 3050,
          top: -80,
          img: 'images/Bäume.png',
          width: 700,
          effects: [
            {
              left: 2000,
              initial: 'animate__scaleTopIn-initial',
              effect: 'animate__scaleTopIn',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 3,
          left: 3100,
          top: 150,
          img: 'images/Katze1.png',
          width: 220
        },
        {
          speed: 0,
          zIndex: 3,
          left: 3270,
          top: 285,
          img: 'images/Curlingstein2.png',
          width: 90,
          effects: [
            {
              left: 2600,
              effect: 'animate__slideRightABit300',
            },
          ],
        },
      ]
    },
    {
      title: 'Minka zeigt, was sie kann',
      color: 'rgb(209, 80, 181)',
      texts: [
        {
          left: 200,
          text: `Für einen Moment war es ganz still.`,
        },
        {
          left: 600,
          text: `Dann brach lauter Jubel aus.`,
        },
        {
          left: 1000,
          text: `Die Tiere konnten es kaum glauben. Die kleine Katze hatte den entscheidenden Wurf geschafft!`,
        },
        {
          left: 1500,
          text: `Der Bär trat vor und sagte: „Wir haben uns geirrt. Auch Katzen können Curling spielen.“`,
        },
        {
          left: 2000,
          text: `Minka lächelte stolz. Sie hatte nicht aufgegeben und an sich geglaubt.`,
        },
        {
          left: 2500,
          text: `Von diesem Tag an spielte sie oft mit den anderen Tieren auf dem Eis.`,
        },
        {
          left: 3200,
          text: `Und immer, wenn neue Schneeflocken vom Himmel fielen, erinnerte sich Minka daran, wie alles begonnen hatte - mit einem Blick aus dem Fenster.`,
        },
      ],
      elements: [
        {
          speed: 0,
          zIndex: 2,
          left: 360,
          top: 100,
          img: 'images/Fuchs1.png',
          width: 250
        },
        {
          speed: 0,
          zIndex: 2,
          left: 610,
          top: 100,
          img: 'images/Fuchs1.png',
          width: 250
        },
        {
          speed: 0,
          zIndex: 2,
          left: 460,
          top: 100,
          img: 'images/Hirsch1.png',
          width: 250
        },
        {
          speed: 0,
          zIndex: 2,
          left: 1260,
          top: 100,
          img: 'images/Fuchs2.png',
          width: 250,
          effects: [
            {
              left: 840,
              effect: 'animate__tada',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 2,
          left: 1510,
          top: 100,
          img: 'images/Fuchs2.png',
          width: 250,
          effects: [
            {
              left: 880,
              effect: 'animate__tada',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 2,
          left: 1360,
          top: 100,
          img: 'images/Hirsch2.png',
          width: 250,
          effects: [
            {
              left: 860,
              effect: 'animate__tada',
            },
          ],
        },
        {
          speed: 0,
          zIndex: 2,
          left: 1700,
          top: -200,
          img: 'images/Baer1.png',
          width: 800
        },
        {
          speed: 0,
          zIndex: 3,
          left: 2500,
          top: 50,
          img: 'images/Katze3.png',
          width: 400
        },
      {
          speed: 0,
          zIndex: 1,
          left: 3000,
          top: -200,
          img: 'images/Curlingbahn.png',
          width: 1000
        },
        {
          speed: 0,
          zIndex: 3,
          left: 4200,
          top: 100,
          img: 'images/Katze3.png',
          width: 400
        },
        {
          speed: 0,
          zIndex: 3,
          left: 4400,
          top: 40,
          img: 'images/Gedankenblase.png',
          width: 250
        },
      ]
    },
  ]
})

function scroll(event) {
  left.value = event.target.scrollLeft
}

onMounted(() => {
  containerRef.value.addEventListener('scroll', scroll)
  pageCenterX.value = window.innerWidth / 2
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
  font-size: 20px;
  line-height: 28px;
}
.textblock::first-letter {
  font-family: 'Georgia', serif;
  font-style: italic;
  font-size: 50px;
  line-height: 28px;
  font-weight: bold;
}

.animate__fadeIn-initial {
  opacity: 0;
}
.animate__scaleTopIn {
  animation-name: scaleTopIn;
}
.animate__scaleTopIn-initial {
  transform: translateY(50%) scaleY(0);
}
@keyframes scaleTopIn {
  0% {
    transform: translateY(50%) scaleY(0);
  }
  80% {
    transform: translateY(-5%) scaleY(1.1);
  }
  100% {
    transform: translateY(0%) scaleY(1);
  }
}

.animate__slideRightABit100 {
  animation-name: slideRightABit100;
}
@keyframes slideRightABit100 {
  0% {
    transform: translateX(0px);
  }
  100% {
    transform: translateX(100px);
  }
}
.animate__slideRightABit {
  animation-name: slideRightABit;
}
@keyframes slideRightABit {
  0% {
    transform: translateX(0px);
  }
  100% {
    transform: translateX(200px);
  }
}
.animate__slideRightABit300 {
  animation-name: slideRightABit300;
}
@keyframes slideRightABit300 {
  0% {
    transform: translateX(0px);
  }
  100% {
    transform: translateX(300px);
  }
}
</style>

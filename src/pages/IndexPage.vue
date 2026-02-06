<template>
  <q-page class="flex flex-center">
    <div class="inhalt">
      <img
        alt="Quasar logo"
        src="src/assets/cat.png"
        class="cat"
      />
      <p>
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr,
        sed diam nonumy eirmod tempor invidunt ut labore et dolore
        magna aliquyam erat, sed diam voluptua. At vero eos et accusam
        et justo duo dolores et ea rebum. Stet clita kasd gubergren,
        no sea takimata sanctus est Lorem ipsum dolor sit amet...
      </p>
      <q-btn color="primary" label="start" to="/page/1" />
    </div>
  </q-page>
</template>

<script setup>
//
</script>

<style lang="css" scoped>
.inhalt {
  width: 400px;
}
.cat {
  width: 200px;
  float: right;
  transform: scaleX(-1);
}
</style>

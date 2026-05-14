<template>
  <q-page class="flex flex-center">
    <div class="inhalt">
      <h1>Minka die Curlingkatze</h1>
      <img
        alt="Quasar logo"
        src="images/Hase.png"
        class="hase"
      />
      <p>
        Klicke auf Start um zu erfahren wie Minka die Curlingwelt endeckt...
      </p>
      <q-btn color="primary" label="start" to="/page/1" />
    </div>
  </q-page>
</template>

<script setup>
//
</script>

<style lang="css" scoped>
h1 {
  margin: 0;
  margin-bottom: 20px;
}
.inhalt {
  width: 500px;
  font-size: 20px;
}
.hase {
  width: 300px;
  float: right;
  transform: scaleX(-1);
}
</style>

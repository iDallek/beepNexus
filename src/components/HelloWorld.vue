<template>
  <v-app id="inspire">
    <v-navigation-drawer
      model-value
      class="pt-4"
      color="grey-darken-4"
      rail
    >
      <v-avatar
        v-for="n in 6"
        :key="n"
        :color="`grey-${n === 1 ? 'darken' : 'lighten'}-1`"
        :size="n === 1 ? 36 : 20"
        class="d-block text-center mx-auto mb-9"
      ></v-avatar>
    </v-navigation-drawer>

    <v-main class="main">
      <div>
        <h2>
          Abastecer Dados
        </h2>
        <v-btn
          class="fuel-btn"
          icon="mdi-database-plus"
        />

      </div>
    </v-main>
  </v-app>
</template>

<style scoped>
.main {
  background-color: #424242;
  color: white;
}

.main div h2 {
  margin: 50px;
  display: inline-block
}

.main .fuel-btn {
  display: inline-block;
}

</style>

<script lang="ts">
  export default {
    //
  }
</script>

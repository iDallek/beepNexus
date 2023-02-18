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
        <v-btn
          class="fuel-btn"
          append-icon="mdi-database-plus"
          @click="dialog=true"
        >
          Abastecer Dados
        </v-btn>
        <ReadSpreadsheetModal
          v-model="dialog"
          @close-dialog="
            dialog = false;
          "
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
.main div {
  margin: 80px;
}

.main .fuel-btn {
  color: #000;
}

</style>

<script lang="ts">
  import ReadSpreadsheetModal from '@/components/ReadSpreadsheetModal.vue'

  export default {
    components: {
      ReadSpreadsheetModal
    },
    data() {
      return {
        dialog: false
      }
    }
  }
</script>

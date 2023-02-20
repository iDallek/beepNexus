<template>
  <v-dialog
    :value="dialog"
    @input="$emit('input', '$event')"
    persistent
  >
    <div class="fileModel">
      <div class="modelContentArea">
        <div class="header">
          <h2 class="me-auto formTitle">
            Adicionar estoque atualizado da loja
          </h2>
          <v-icon
            icon="mdi-close"
            class="restartIcon"
          />
        </div>
        <div class="draggableArea">
          <v-icon
            icon="mdi-upload"
            size="35"
            class="uploadIcon"
          />
          <p class="infoText">
            Arraste e solte ou <span>Escolhe um arquivo</span> para enviar
          </p>
          <p class="extensionsInfo">XLSX or ODD</p>
        </div>
        <v-btn color="error" @click="close">Close</v-btn>
      </div>
    </div>
  </v-dialog>
</template>
<script lang="ts">

export default {
  props: {
    dialog: Boolean,
  },
  methods: {
    close() {
      this.$emit("close-dialog")
    }
  }
}
</script>
<style>
  .fileModel {
    background-color: #221F25;
    color: white;
    border-radius: 10px;
    min-width: 650px;
    max-width: 800px;
    width: 55%;
    margin: auto;
  }

  .modelContentArea {
    margin: 30px 45px;
    background-color: transparent;
    color: rgba(255, 255, 255, 0.8);
  }

  .modelContentArea .header {
    display: flex;
  }

  .formTitle {
    background-color: transparent;
    margin: auto 0;
    padding: 0;
    width: 80%;
    font-weight: 400;
    font-size: 1.2em;
  }

  .restartIcon {
    background-color: transparent;
    display: inline-block;
    cursor: pointer;
    margin: auto 0;
    margin-left: auto;
  }

  .draggableArea {
    background-color: transparent;
    height: 250px;
    margin: 30px 0;
    background-image: url("data:image/svg+xml,%3csvg width='100%25' height='100%25' xmlns='http://www.w3.org/2000/svg'%3e%3crect width='100%25' height='100%25' fill='none' rx='10' ry='10' stroke='%23FFFFFF12' stroke-width='4' stroke-dasharray='6%2c 14' stroke-dashoffset='0' stroke-linecap='square'/%3e%3c/svg%3e");
    border-radius: 10px;
    text-align: center;
  }

  .draggableArea .uploadIcon {
    margin-top: 55px;
    background-color: transparent;
    display: inline-block;
    color: rgba(255, 255, 255, 0.2);
  }

  .draggableArea .infoText {
    margin: 20px;
  }

  .draggableArea .infoText span {
    color: #3E84C6;
    cursor: pointer;
  }

  .draggableArea .extensionsInfo {
    color: rgba(255, 255, 255, 0.2);
    font-size: 0.9em;
  }

</style>

<template>
  <div
    class="dropArea"
    @dragover="dragover"
    @drop="drop"
  >
    <input
      type="file"
      class="input"
      id="dropFieldHandle"
      ref="file"
      @change="onChange"
    />
    <v-icon
      icon="mdi-upload"
      size="35"
      class="uploadIcon"
    />
    <label for="dropFieldHandle">
      <span class="infoText">
        Arraste e solte ou <span>Escolhe um arquivo</span> para enviar
      </span>
    </label>
    <span class="extensionsInfo">XLSX or ODD</span>
    <div @dragleave="dragleave" class="dropPopup" />
  </div>
</template>
<script lang="ts">

function dragover(event : any) : void {
  event.preventDefault()

  const types = event.dataTransfer.items.length
  types != 1 ? console.log("Erro: Mova apenas 1 arquivo por vez.") :
  console.log("Jogar")

  this.$el.querySelector(".dropPopup").style.setProperty('display', 'block')

  // if (!event.currentTarget.classList.contains('bgBlue')) {
  //   event.currentTarget.classList.add('bgBlue')
  // }
}

function dragleave(event : any) : void {
  // console.log('saiu')

  this.$el.querySelector(".dropPopup").style.setProperty('display', 'none')
}

function drop(event : any) : void {
  event.preventDefault()

  this.$refs.file.files = event.dataTransfer.files
  // 1# Refatorar
  onChange(event, 'manual')

  event.currentTarget.classList.remove('bgBlue')
}

function onChange(e: any, isManual?: string) : void {
  // 1# Refatorar
  isManual ? console.log("Drop", e.dataTransfer?.files) :
  console.log("Click", this.$refs.file.files)
}

export default {
  methods: {
    dragover,
    dragleave,
    drop,
    onChange
  }
}
</script>
<style>

.dropArea {
    background-color: transparent;
    height: 250px;
    margin: 30px 0;
    background-image: url("data:image/svg+xml,%3csvg width='100%25' height='100%25' xmlns='http://www.w3.org/2000/svg'%3e%3crect width='100%25' height='100%25' fill='none' rx='10' ry='10' stroke='%23FFFFFF12' stroke-width='4' stroke-dasharray='6%2c 14' stroke-dashoffset='0' stroke-linecap='square'/%3e%3c/svg%3e");
    border-radius: 10px;
    text-align: center;
    display: block;
    position: relative;
  }

  .dropArea input {
    display: none;
    position: relative;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }

  .dropArea .uploadIcon {
    margin-top: 55px;
    background-color: transparent;
    display: inline-block;
    color: rgba(255, 255, 255, 0.2);
  }

  .dropArea .infoText {
    display: block;
    margin: 20px;
  }

  .dropArea .infoText span {
    color: #3E84C6;
    cursor: pointer;
  }

  .dropArea .extensionsInfo {
    color: rgba(255, 255, 255, 0.2);
    font-size: 0.9em;
  }

  .dropArea .dropPopup {
    display: none;
    box-sizing: content-box;
    position: absolute;
    width: 100%;
    top: 0;
    left: 0;
    background-color: rgba(0, 153, 255, 0.05);
    height: 100%;
    border-radius: 10px;
    z-index: 20;
  }

  .bgBlue {
    background-color: rgba(0, 153, 255, 0.05);
  }

</style>

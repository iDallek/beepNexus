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
// const statusDragAndDropArea =

function validationDragoverFile (event: any, element: any) {
  const propsToValidate = {
    quantityFiles: event.dataTransfer.items.length,
    type: event.dataTransfer.items[0].type
  }

  const validCases = {
    "Valid": (el: Element): void => {
      el.classList.remove('bgRed')
      el.classList.add('bgBlue')
    },
    "Invalid, only 1 file": (el: Element): void => {
      el.classList.remove('bgBlue')
      el.classList.add('bgRed')
    },
    "Invalid, file extentesion is not XLSX or ODD": (el: Element): void => {
      el.classList.remove('bgBlue')
      el.classList.add('bgRed')
    }
  }

  const validType = "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"

  let validation

  if (propsToValidate.quantityFiles !== 1) {
    validation = "Invalid, only 1 file"
  } else if (propsToValidate.type !== validType) {
    validation = "Invalid, file extentesion is not XLSX or ODD"
  } else {
    validation = "Valid"
  }

  validCases[validation as keyof Object](element)
}

function dragover(event : any) : void {
  event.preventDefault()
  const element = this.$el.querySelector(".dropPopup")

  const validationResult = validationDragoverFile(event, element)

  // if (validationResult === "Valid") {
  //   this.$el.querySelector(".dropPopup").classList.remove('bgRed')
  //   this.$el.querySelector(".dropPopup").classList.add('bgBlue')
  // } else {
  //   this.$el.querySelector(".dropPopup").classList.remove('bgBlue')
  //   this.$el.querySelector(".dropPopup").classList.add('bgRed')
  // }

  this.$el.querySelector(".dropPopup").style.setProperty('display', 'block')
}

function dragleave() : void {
  this.$el.querySelector(".dropPopup").style.setProperty('display', 'none')
}

function drop(event : any) : void {
  event.preventDefault()

  this.$refs.file.files = event.dataTransfer.files
  // 1# Refatorar
  onChange(event, 'manual')

  this.$el.querySelector(".dropPopup").style.setProperty('display', 'none')
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
    /* background-color: rgba(0, 153, 255, 0.05); */
    height: 100%;
    border-radius: 10px;
    z-index: 20;
  }

  .bgBlue {
    background-color: rgba(0, 153, 255, 0.05);
  }

  .bgRed {
    background-color: rgba(255, 0, 0, 0.05);
  }

</style>

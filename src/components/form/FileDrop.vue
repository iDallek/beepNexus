<template>
  <div
    class="dropArea"
    @dragover="dragover"
    @drop="drop"
  >
    <FileDropCases v-if="vueStore === 'Valid'" :content="contentToDrapAndDrop[vueStore]" :funcOnChange="onChange"  />
    <FileDropCases v-else-if="vueStore === 'Invalid, only 1 file'" :content="contentToDrapAndDrop[vueStore]" :funcOnChange="onChange"  />
    <FileDropCases v-else-if="vueStore === 'Invalid, file extentesion is not XLSX or ODD'" :content="contentToDrapAndDrop[vueStore]" :funcOnChange="onChange"  />
    <div>
      <input
        type="file"
        class="input"
        id="dropFieldHandle"
        ref="file"
        accept="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
        @change="onChange"
      />
      <v-icon
        size="35"
        class="uploadIcon"
      >
        {{ this.contentToDrapAndDrop[vueStore]?.iconId || 'mdi-upload'  }}
      </v-icon>
      <label for="dropFieldHandle">
        <span class="infoText">
          Arraste e solte ou <span>Escolhe um arquivo</span> para enviar
        </span>
      </label>
      <span class="extensionsInfo">XLSX or ODD</span>
      <div @dragleave="dragleave" class="dropPopup" />
    </div>
  </div>
</template>
<script lang="ts">
let vueStore = ''

const contentToDrapAndDrop = {
  "Valid": {
    iconId: "mdi-upload",
    text: "Solte para enviar"
  },
  "Invalid, only 1 file": {
    iconId: "mdi-close",
    text: "Arraste apenas 1 arquivo"
  },
  "Invalid, file extentesion is not XLSX or ODD": {
    iconId: "mdi-close",
    text: "Extensão do arquivo incompatível"
  }
}

function validationDragoverFile (event: any, element: any, t: any) {
  const propsToValidate = {
    quantityFiles: event.dataTransfer.items.length,
    type: event.dataTransfer.items[0].type
  }

  
  const validCases = {
    "Valid": ({element, validation}: any): void => {
      element.classList.remove('bgRed')
      element.classList.add('bgBlue')
      
      setDragCase(validation)
    },
    "Invalid, only 1 file": ({element, validation}: any): void => {
      element.classList.remove('bgBlue')
      element.classList.add('bgRed')
      
      setDragCase(validation)
    },
    "Invalid, file extentesion is not XLSX or ODD": ({element, validation}: any): void => {
      element.classList.remove('bgBlue')
      element.classList.add('bgRed')
      
      setDragCase(validation)
    }
  }
  
  const acceptExtensionsTypes = [
    "application/vnd.oasis.opendocument.spreadsheet",
    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
  ]
  
  let validation
  
  let shouldSkip = false;
  acceptExtensionsTypes.forEach((validType, index, array) => {

    if (shouldSkip) {
      return
    }

    if (propsToValidate.quantityFiles !== 1) {
      validation = "Invalid, only 1 file"
    } else if (propsToValidate.type !== validType) {
      validation = "Invalid, file extentesion is not XLSX or ODD"
    } else {
      validation = "Valid"
      shouldSkip = true
    }
  })
  
  validCases[validation as unknown as keyof Object]({ element, validation } as unknown as PropertyKey)
  t.vueStore = vueStore
}

function dragover(event : any) : void {
  event.preventDefault()
  const element = this.$el.querySelector(".dropPopup")

  validationDragoverFile(event, element, this)

  this.$el.querySelector(".dropPopup").style.setProperty('display', 'block')
}

function dragleave() : void {
  this.$el.querySelector(".dropPopup").style.setProperty('display', 'none')
  this.vueStore = ''
  setDragCase('')
}

function drop(event : any) : void {
  event.preventDefault()
  this.$refs.file.files = event.dataTransfer.files

  onChange(event, "Manual")

  // 1# Refatorar
  this.$el.querySelector(".dropPopup").style.setProperty('display', 'none')
  setDragCase('')
}

async function onChange(e: any, isManual?: string) : Promise<void> {
  if (isManual) {
    const f = e.dataTransfer?.files[0]
    const data = await f.arrayBuffer()

    console.log("Drop", data)
  } else {
    const f = this.$refs.file.files[0]
    const data = await f.arrayBuffer()

    console.log("Click", data)
  }

  // 1# Refatorar
  // isManual ? console.log("Drop", e.dataTransfer?.files) :
  // console.log("Click", this.$refs.file.files)
}

function setDragCase(dragCase: string): void {
  vueStore = dragCase
}

function getDragCase(): any {
  return vueStore
}

import FileDropCases from '@/components/form/FileDropCases.vue'

export default {
  data() {
    return {
      vueStore,
      contentToDrapAndDrop
    }
  },
  methods: {
    dragover,
    dragleave,
    drop,
    onChange,
    setDragCase,
    getDragCase
  },
  components: {
    FileDropCases
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
    /* background-color: transparent; */
    display: inline-block;
    color: rgb(83, 83, 83);
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

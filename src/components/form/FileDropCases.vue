<template>
  <div class="dragCaseArea">
    <input
      type="file"
      class="input"
      id="dropFieldHandle"
      ref="file"
      accept="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
      @change="funcOnChange"
      />
      <v-icon
        size="35"
        class="uploadIcon"
      >
       {{ content.iconId }}
      </v-icon>
      <label for="dropFieldHandle">
        <span class="infoText">
          {{ content.text }}
        </span>
      </label>
      <span class="extensionsInfo">XLSX or ODD</span>
  </div>
</template>
<script lang="ts">

export default {
  props: ['content', 'funcOnChange']
}
</script>
<style>
  .dragCaseArea {
    position: absolute;
    background-image: url("data:image/svg+xml,%3csvg width='100%25' height='100%25' xmlns='http://www.w3.org/2000/svg'%3e%3crect width='100%25' height='100%25' fill='none' rx='10' ry='10' stroke='%23FFFFFF12' stroke-width='4' stroke-dasharray='6%2c 14' stroke-dashoffset='0' stroke-linecap='square'/%3e%3c/svg%3e");
    background-color: #221F25;
    width: 100%;
    height: 100%;
  }
</style>
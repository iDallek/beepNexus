<template>
  <v-dialog
    :value="dialog"
    @input="$emit('input', '$event')"
    persistent
  >
    <v-card>
      <v-card-title primary-title>
        Modal Content
      </v-card-title>
      <v-card-text>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
      </v-card-text>
      <v-divider />
      <v-card-actions>
        <v-spacer />
        <v-btn color="error" @click="close">Close</v-btn>
      </v-card-actions>
    </v-card>
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

</style>

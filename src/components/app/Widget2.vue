<template>
  <div style="display: flex; flex-direction: column">
    <v-textarea
        hint="Send Anthony a message"
        label="Anthony Sebastian"
        name="input-7-1"
        value="The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.">

    </v-textarea>
    <div style="display: flex; flex-direction: row">
      <div style="flex: auto 1 1"></div>
      <v-btn color="deep-purple accent-4" text>
        Send
      </v-btn>
    </div>

  </div>
</template>

<script>
export default {
  name: "Widget2",
  inject: ['$dashPanelEvents'],
  created() {

    this.$dashPanelEvents().$on('share', () => {
      console.log('onPanelShare');
    });

    this.$dashPanelEvents().$on('refresh', () => {
      this.getData();
    });

    this.$dashPanelEvents().$on('close', () => {
      console.log('onPanelClose');
    })
  },
  methods: {
    getData() {
      this.$dashPanelEvents().$emit('loading', true);
      setTimeout(() => this.$dashPanelEvents().$emit('loading', false), 1000);
    }
  }
}
</script>

<style scoped>

</style>

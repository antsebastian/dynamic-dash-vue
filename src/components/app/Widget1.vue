<template>
  <v-timeline
      align-top
      dense
  >
    <v-timeline-item
        color="pink"
        small
    >
      <v-row class="pt-1">
        <v-col cols="3">
          <strong>5pm</strong>
        </v-col>
        <v-col>
          <strong>New Icon</strong>
          <div class="caption">Mobile App</div>
        </v-col>
      </v-row>
    </v-timeline-item>

    <v-timeline-item
        color="teal lighten-3"
        small
    >
      <v-row class="pt-1">
        <v-col cols="3">
          <strong>3-4pm</strong>
        </v-col>
        <v-col>
          <strong>Design Stand Up</strong>
        </v-col>
      </v-row>
    </v-timeline-item>

    <v-timeline-item
        color="pink"
        small
    >
      <v-row class="pt-1">
        <v-col cols="3">
          <strong>12pm</strong>
        </v-col>
        <v-col>
          <strong>Lunch break</strong>
        </v-col>
      </v-row>
    </v-timeline-item>

    <v-timeline-item
        color="teal lighten-3"
        small
    >
      <v-row class="pt-1">
        <v-col cols="3">
          <strong>9-11am</strong>
        </v-col>
        <v-col>
          <strong>Finish Home Screen</strong>
          <div class="caption">Web App</div>
        </v-col>
      </v-row>
    </v-timeline-item>
  </v-timeline>
</template>

<script>

export default {
  name: "Widget1",
  inject: ['$dashPanelEvents'],

  created() {

    this.$dashPanelEvents().$on('share', () => console.log('onPanelShare'));

    this.$dashPanelEvents().$on('refresh', () => this.getData());

    this.$dashPanelEvents().$on('close', () => console.log('onPanelClose'));
  },
  methods: {
    getData() {
      this.$dashPanelEvents().$emit('loading', true);
      setTimeout(() => this.$dashPanelEvents().$emit('loading', false), 2000);
    }
  }
}
</script>

<style scoped>

</style>

<template>
  <div>
    <v-card :disabled="loadingData" :loading="loadingData">
      <v-card-title>
        <v-icon>{{ panelConfig.icon }}</v-icon>
        <h4 class="title">{{ panelConfig.title }}</h4>
        <v-spacer></v-spacer>
        <v-menu bottom left>
          <template v-slot:activator="{ on }">
            <v-btn icon v-on="on">
              <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
          </template>
          <v-list>
            <v-list-item @click="onShare()">
              <v-list-item-icon>
                <v-icon>mdi-share-variant</v-icon>
              </v-list-item-icon>
              <v-list-item-title>Share</v-list-item-title>
            </v-list-item>
            <v-list-item @click="onRefresh()">
              <v-list-item-icon>
                <v-icon>mdi-refresh</v-icon>
              </v-list-item-icon>
              <v-list-item-title>Refresh</v-list-item-title>
            </v-list-item>
            <v-list-item @click="onClose()">
              <v-list-item-icon>
                <v-icon>mdi-close</v-icon>
              </v-list-item-icon>
              <v-list-item-title>Close</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-card-title>
      <div style="padding-bottom: 16px; padding-left: 16px; padding-right: 16px">
        <v-skeleton-loader class="mx-auto"
                           type="card"
                           v-if="showSkeletor"
        ></v-skeleton-loader>
        <component :style="showSkeletor ? {display: 'none'} : {display: 'block'}" v-bind:is="widget"></component>
      </div>
    </v-card>
  </div>
</template>

<script>
import Vue from 'vue'

export default {
  name: "Panel",
  props: {
    panelConfig: Object,
  },

  data() {
    return {
      widget: null,
      panelEvents: new Vue({}),
      loadingData: false,
      showSkeletor: true,
    }
  },
  provide() {
    return {
      $dashPanelEvents: () => this.panelEvents,
    };
  },
  mounted() {
    import(`../app/${this.panelConfig.widget.name}.vue`).then((module) => {
      this.widget = Vue.component(
          this.panelConfig.widget.name,
          module
      ).default;

      this.$nextTick(() => this.onRefresh());

    });

    this.panelEvents.$on('loading', (isLoading) => {
      if (!isLoading) { //keep skeletor until first data load complete so the view doesn't jump around
        this.showSkeletor = false;
      }
      if (!this.showSkeletor) { //show progress only on subsequent data calls
        this.loadingData = isLoading;
      }
    })
  },
  methods: {
    onShare() {
      this.panelEvents.$emit('share');
    },
    onRefresh() {
      this.panelEvents.$emit('refresh');
    },
    onClose() {
      this.panelEvents.$emit('close');
    }
  }
}
</script>

<style lang="scss" scoped>
.title {
  margin-left: 10px;
}

</style>

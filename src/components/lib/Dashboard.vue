<template>
  <v-content>
    <div class="grid-container grid-gaps">
      <panel :key="p.title" :panelConfig="p" :style="$vuetify.breakpoint.xsOnly ? {} :
                            { gridColumn: p.position.col + ' / span ' + p.position.colSpan,
                            gridRow: p.position.row + ' / span ' + p.position.rowSpan }"
             style="display: grid"
             v-for="p in dashboardConfig.panels">
      </panel>
    </div>
  </v-content>
</template>

<script>
import Panel from "@/components/lib/Panel";

export default {

  components: {
    'panel': Panel
  },
  props: {
    dashboardConfig: Object,
  },

  name: 'DashboardGrid',
}
</script>
<style lang="scss" scoped>
@import '../../../node_modules/vuetify/src/styles/styles';

.grid-gaps {
  grid-gap: 32px;
  padding-left: 64px;
  padding-right: 64px;
  padding-bottom: 64px;
}

@media #{map-get($display-breakpoints, 'xs-only')} {

  .grid-gaps {
    grid-gap: 16px;
    padding-left: 24px;
    padding-right: 24px;
    grid-template-columns: 100%;
    grid-auto-flow: row;
  }
}

@media #{map-get($display-breakpoints, 'sm-only')} {

  .grid-gaps {
    grid-gap: 24px;
    padding-left: 32px;
    padding-right: 32px;
  }
}

.grid-container {
  display: grid;
  grid-auto-rows: max-content;
  max-width: 1200px;
}

</style>

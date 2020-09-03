# Dynamic Dashboard Vue

A Vue component that loads and positions panels based on json data and dynamically loads a widget into each panel.
![alt text](./src/assets/loaded.png)

## Dynamically Loading the Widget

The panel binds its widget property to the 'is' property of Vue's component tag. 
When the panel mounts, it loads the widget using webpack's dynamic import, it then sets the widget property to the loaded widget component.


[see Panel.Vue](./src/components/lib/Panel.vue)
```        
    // binding to the component tag
    <component :style="showSkeletor ? {display: 'none'} : {display: 'block'}" v-bind:is="widget"></component>

    //on mounted, the panel loads the widget and then sets the widget property
    import(`../app/${this.panelConfig.widget.name}.vue`).then((module) => {
      this.widget = Vue.component(
          this.panelConfig.widget.name,
          module
      ).default;

```
##Layout Alg
Dashboard loops through the panels collection defined in [dashboard.json](./src/assets/mock-data/dashboard.json)
 and adds each [Panel.Vue](./src/components/lib/Panel.vue) component to the main css grid and then binds the grid properties. 

[see Dashboard.Vue](./src/components/lib/Dashboard.vue)

## Dependency injection
Dashboard uses Vue's dependency injection (new feature Vue.js 3.x) to facilitate scoped communication between the panel and widget components. 

##UX - Skeleton and...TBD  

![alt text](./src/assets/loading-skeletons.png)

![alt text](./src/assets/user-panel-refresh.png)

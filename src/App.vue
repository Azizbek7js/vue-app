<template>
  <div class="viewport">
    <SideBar :route="route" @update-route='updateRoute'/>
    <div class="content">
      <div class="main-container">
          <TableComponent v-if="route==='table'"/>
          <InputComponent v-if="route==='input'" />
          <TabsComponent v-if="route === 'tabs'"/>
          <PanelComponent v-if="route==='panel'"/>
        </div>
    </div>
  </div>
</template>

<script>
import SideBar from "@/components/sidebar/SideBar.vue";
import TableComponent from "@/components/table/TableComponent.vue"
import InputComponent from "@/components/input/InputComponent.vue";
import TabsComponent from "@/components/tabs/TabsComponent.vue";
import PanelComponent from "@/components/panel/PanelComponent.vue";
export default {
  name: 'App',
  components: {
    PanelComponent,
    TabsComponent,
    InputComponent,
    TableComponent,
    SideBar,
  },
  data() {
    return {
      route: 'main',
    }
  },
  methods: {
    updateRoute(route){
      this.route = route
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Roboto:300,400,400i,500');

body {
  overflow-x: hidden;
  font-family: 'Roboto', sans-serif;
  font-size: 16px;
}

.main-container{
  width: fit-content;
  padding: 30px;
}
.content {
  width: 100%;
  position: relative;
  margin-right: 0;
}
.viewport {
  padding-left: 250px;
  -webkit-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
  -o-transition: all 0.5s ease;
  transition: all 0.5s ease;
}
</style>
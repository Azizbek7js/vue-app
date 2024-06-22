<template>
  <div class="pt-4" style="height: 400px;">
    <input type="checkbox" v-model="allShowItems">
    <div class="category border rounded px-4 py-2" v-for="item in itemsComputed" :key="item.name" :class="{'my-3': item.isOpen === true}">
      <div class="d-flex align-items-center justify-content-between" @click="toggleOpen(item)">
        <span>{{item.name}}</span>
        <i :class="{'fas fa-chevron-down small': item.isOpen === false, 'fas fa-chevron-up small': item.isOpen === true}"></i>
      </div>
      <p class="pt-2" v-if="item.isOpen">{{item.text}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PanelComponent',
  data(){
    return{
      showBottom:false,
      items:[
        {name: 'item-1' , isOpen: false , text:'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat' },
        {name: 'item-2' , isOpen: false , text:'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat' },
        {name: 'item-3' , isOpen: false , text:'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat' },
        {name: 'item-4' , isOpen: false , text:'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat' }
      ],
      allShowItems:false,
    }
  },
  computed: {
    itemsComputed() {
      return this.items;
    }
  },
  watch:{
    allShowItems(val){
      if(val){
        this.items.map(item => item.isOpen = true)
      }else {
        this.items.map(item => item.isOpen = false)
      }
    }
  },
  methods: {
    toggleOpen(item){
      this.items = this.items.map(t =>{
        if(t.name === item.name){
          return {
            ...t,
            isOpen: !item.isOpen
          }
        }else{
          return {
            ...t,
            isOpen: false
          }
        }
      })
    },
  }
}
</script>

<style scoped>
.category{
  width: 600px;
  transition: all 0.25s;
}

</style>
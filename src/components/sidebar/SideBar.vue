<template>
  <div class="sidebar">
    <header>
      <a @click="$emit('update-route', 'main')">My App</a>
    </header>
    <ul class="box">
      <li @click="$emit('update-route', 'table')" class="rounded mt-2" :class="{'bg-primary': route==='table'}">
        <a>
          <i class="fas fa-1"></i> Table
        </a>
      </li>
      <li @click="$emit('update-route', 'input')" class="rounded" :class="{'bg-primary': route==='input'}">
        <a>
          <i class="fas fa-2"></i> Input
        </a>
      </li>
      <li @click="$emit('update-route', 'tabs')" class="rounded" :class="{'bg-primary': route==='tabs'}">
        <a>
          <i class="fas fa-3"></i> Tabs
        </a>
      </li>
      <li @click="$emit('update-route', 'panel')" class="rounded" :class="{'bg-primary': route==='panel'}">
        <a>
          <i class="fas fa-4"></i> Panel
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'SideBar',
  props: {
    route: {
      type: String,
      required: true
    }
  }
}
</script>
<style scoped>
.sidebar {
  z-index: 1000;
  position: fixed;
  left: 250px;
  width: 250px;
  height: 100%;
  margin-left: -250px;
  overflow-y: auto;
  background: #37474F;
  -webkit-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
  -o-transition: all 0.5s ease;
  transition: all 0.5s ease;
}
.sidebar header {
  background-color: #263238;
  font-size: 20px;
  line-height: 52px;
  text-align: center;

}

.sidebar header a {
  color: #fff;
  display: block;
  cursor: pointer;
  text-decoration: none;
}

.sidebar header a:hover {
  color: #fff;
}

.sidebar .box{
  width: 215px;
  display: flex;
  flex-direction: column;
  gap: 20px;
  li{
    width: 100%;
    padding: 10px;
    list-style: none;
  }
}

.sidebar .box a{
  background: none;
  color: #CFD8DC;
  cursor: pointer;
  font-size: 14px;
  display: block;
  text-decoration: none;
}

.sidebar .box a:hover{
  background: none;
  color: #ECEFF1;
}

.sidebar .box a i{
  margin-right: 16px;
}

</style>
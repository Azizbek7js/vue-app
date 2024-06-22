<template>
  <div v-if="modalOpen" class="modal-container" >
    <div class="modal-content"  @click.self="closeModal">
      <table class="bordered" style="width: 100%;">
        <thead>
        <tr>
          <th>Header Name</th>
          <th>Size (px)</th>
        </tr>
        </thead>
        <draggable v-model="header" :list="header" group="columns" :element="'tbody'">
          <tr v-for="column in header" :key="column.key">
            <td>
              <input v-model="column.name" />
            </td>
            <td>
              <input v-model="column.size" type="number" />
            </td>
          </tr>
        </draggable>
      </table>
      <div style="margin-top: 20px;">
        <button @click="closeModal">Save</button>
      </div>
    </div>
  </div>
</template>
<script>
import draggable from 'vuedraggable';
  export default {
  name: "ModalComponent",
  components:{draggable},
  watch: {
    header: {
      handler() {
        localStorage.setItem('header', JSON.stringify(this.header));
      },
      deep: true
    },
  },
  data(){
    return{
      header:[],
      modalOpen: false,
    }
  },
  mounted() {
    document.addEventListener('keydown', this.handleKeydown);
  },
  beforeDestroy() {
    document.removeEventListener('keydown', this.handleKeydown);
  },
  methods:{
    openModal(header) {
      this.header = header
      this.modalOpen = true;
    },
    closeModal() {
      this.modalOpen = false;
    },
    handleKeydown(event) {
      if (event.key === 'Escape') {
        this.closeModal();
      }
      if(event.key === 'Enter') {
        this.closeModal();
      }
    }
  }
}

</script>
<style scoped>
.modal-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  z-index: 15;
  width: 80%;
  max-width: 600px;
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
}
</style>
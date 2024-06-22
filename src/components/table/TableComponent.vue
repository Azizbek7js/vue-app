<template>
  <div>
    <input type="text" class="inputSearch" v-model="search" placeholder="Search...">
    <div class="pt-2">
      <button class="btn btn-primary" @click="changeStatus('ALL')">ALL</button>
      <button class="btn btn-success mx-2" @click="changeStatus('ACTIVE')">ACTIVE</button>
      <button class="btn btn-danger" @click="changeStatus('INACTIVE')">INACTIVE</button>
    </div>
    <div class="table-container">
      <div>
        <table class="bordered">
          <thead>
          <tr>
            <th v-for="column in displayedColumns" :key="column.name" :style="{ width: column.size < 1000 ? column.size + 'px': '1000px' }">{{ column.name }}</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="data in filteredData" :key="data.id">
            <td v-for="column in displayedColumns" :key="`${data.id}-${column.key}`">{{ data[column.key] }}</td>
          </tr>
          </tbody>
        </table>
        <div class="d-flex align-items-center justify-content-end p-2">
          <button class="btn border rounded mx-1" v-for="pageNumber in pages" @click="page = pageNumber" :class="{'btn-primary':pageNumber === page}" :key="pageNumber">{{pageNumber}}</button>
        </div>
      </div>
      <div class="checkbox-container">
        <div v-for="item in header" :key="item.name" class="checkbox-item">
          <input type="checkbox" v-model="item.check" />
          <i class="fas fa-pencil-alt edit" @click="openModal"></i>
          <p>{{ item.name }}</p>
        </div>
      </div>
    </div>
    <ModalComponent ref="modalComponent"/>
  </div>
</template>

<script>

import ModalComponent from "@/components/ModalComponent.vue";

export default {
  name: 'TableComponent',
  components: {ModalComponent},
  data(){
    return {
      header: [
        { name: 'Name', key: 'name', check: true, size: 20 },
        { name: 'Age', key: 'age', check: true, size: 10 },
        { name: 'Email', key: 'email', check: true, size: 30 },
        { name: 'Email', key: 'email', check: true, size: 30 },
        { name: 'Status', key: 'status', check: true, size: 20 },
        { name: 'Occupation', key: 'occupation', check: true, size: 20 }
      ],
      tableData: [
        { id: 1, name: 'John Doe', age: 30,status: 'ACTIVE', email: 'john@example.com', country: 'USA', occupation: 'Engineer' },
        { id: 2, name: 'Jane Smith', age: 25,status: 'ACTIVE', email: 'jane@example.com', country: 'Canada', occupation: 'Doctor' },
        { id: 3, name: 'Bob Johnson', age: 35,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 4, name: 'Bob Johnson', age: 35,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 5, name: 'Jane Smith', age: 25,status: 'ACTIVE', email: 'jane@example.com', country: 'Canada', occupation: 'Doctor' },
        { id: 6, name: 'Bob Johnson', age: 35,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 7, name: 'Bob Johnson', age: 35,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 8, name: 'Bob Johnson', age: 35,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 9, name: 'Bob Johnson', age: 35,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 10, name: 'Bob Johnson', age: 35,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 11, name: 'Bob ', age: 22,status: 'INACTIVE' , email: 'jane@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 12, name: ' Johnson', age: 35,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 13, name: 'Bob Johnson', age: 10,status: 'INACTIVE' , email: 'bob@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 14, name: 'Jane Smith', age: 15,status: 'INACTIVE' , email: 'jane@example.com', country: 'UK', occupation: 'Teacher' },
        { id: 15, name: 'Bob Johnson', age: 35,status: 'INACTIVE' , email: 'jane@example.com', country: 'UK', occupation: 'Teacher' },
      ],
      status:'ALL',
      search: '',
      page: 1,
      perPage: 5,
      pages: [],
    }
  },
  watch:{
    posts () {
      this.setPages();
    },
  },
  mounted() {
    this.setPages()
    this.header = JSON.parse(localStorage.getItem('header')) || this.header;
  },
  computed: {
    displayedColumns() {
      return this.header.filter(item => item.check);
    },
    filteredData() {
      const status = this.status;
      const search = this.search.toLowerCase();
      let page = this.page;
      let perPage = this.perPage;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);
      let data = this.tableData.slice(from, to);
      return data.slice().sort((a, b) => a.age - b.age).filter(item => {
        if (status !== 'ALL' && item.status !== status) {
          return false;
        }
        return Object.values(item).some(value => String(value).toLowerCase().includes(search));
      });
    }
  },
  methods: {
    changeStatus(status){
      this.status = status
    },
    openModal(){
      this.$refs.modalComponent.openModal(this.header)
    },
    setPages () {
      let numberOfPages = Math.ceil(this.tableData.length / this.perPage);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
  }
}
</script>

<style scoped>
.table-container {
  max-width: 1920px;
  height: auto;
  display: flex;
  gap: 20px;
  margin-top: 20px;
  text-align: center;
}


table.bordered {
  border-collapse: collapse;
  border: 1px solid #ddd;
}

table.bordered th,
table.bordered td {
  padding: 10px;
  border: 1px solid #ddd;
}

.checkbox-container {
  display: flex;
  flex-direction: column;
}

.checkbox-item {
  display: flex;
  align-items: center;
  gap: 10px;
}

.checkbox-item input {
  margin-right: 5px;
}
.edit {
  cursor: pointer;
  font-size: 13px;
  color: rgb(255, 136, 0);
}
.inputSearch {
  position: relative;
  width: 300px;
  margin-top: 10px;
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  transition: border-color 0.3s, box-shadow 0.3s;
}


</style>

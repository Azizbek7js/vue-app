<template>
  <div>
    <div class="header">
      <button @click="showModal = true">Modal</button>
    </div>
    <div  class="table-container">
      <table class="bordered">
        <thead>
          <tr>
            <th v-for="column in displayedColumns" :key="column.name">{{ column.name }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in tableData" :key="data.id">
            <td v-for="column in displayedColumns" :key="column.key">{{ data[column.key] }}</td>
          </tr>
        </tbody>
      </table>
      <div class="checkbox-container">
        <div v-for="item in header" :key="item.name" class="checkbox-item">
          <input type="checkbox" v-model="item.check" />
          <p>{{ item.name }}</p>
        </div>
      </div>
    </div>
    <div v-if="showModal" class="modal-container">
      <div class="modal-content">
        <h2>Modal Title</h2>
        <p>This is the modal content.</p>
        <button @click="showModal = false">Close</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      showModal: false,
      header:[
        { name: 'Name', key: 'name', check: true},
        { name: 'Age', key: 'age', check: true},
        { name: 'Email', key: 'email', check: true},
        { name: 'Country', key: 'country', check: true},
        { name: 'Occupation', key: 'occupation', check: true},
      ],
      tableData: [
      { id: 1, name: 'John Doe', age: 30, email: 'john@example.com', country: 'USA', occupation: 'Engineer' },
      { id: 2, name: 'Jane Smith', age: 25, email: 'jane@example.com', country: 'Canada', occupation: 'Doctor' },
      { id: 3, name: 'Bob Johnson', age: 35, email: 'bob@example.com', country: 'UK', occupation: 'Teacher' }
      ]
    }
  },
  computed: {
    displayedColumns() {
      return this.header.filter(item => item.check);
    }
  }
}
</script>

<style>
.header {
  width: 100%;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.table-container {
  display: flex;
  gap: 200px;

  margin-top: 20px;
  text-align: center;
}

table.bordered {
  width: 60%;
  border-collapse: collapse;
  border: 1px solid #ddd;
}

table.bordered th, table.bordered td {
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
}

.checkbox-item input {
  margin-right: 5px;
}


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
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
}
</style>
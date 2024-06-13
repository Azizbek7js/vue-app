<template>
  <div>
    <div class="header">
    </div>
    <div class="table-container">
      <table class="bordered">
        <thead>
          <tr>
            <th v-for="column in displayedColumns" :key="column.name">{{ column.name }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in tableData" :key="data.id">
            <td v-for="column in displayedColumns" :key="`${data.id}-${column.key}`" :style="{ width: column.size+ 'px' }">{{ data[column.key] }}</td>
          </tr>
        </tbody>
      </table>
      <div class="checkbox-container">
        <div v-for="item in header" :key="item.name" class="checkbox-item">
          <input type="checkbox" v-model="item.check" />
          <i class="fas fa-pencil-alt edit" @click="showModal = true"></i>
          <p>{{ item.name }}</p>
        </div>
      </div>
    </div>
    <div v-if="showModal" class="modal-container">
      <div class="modal-content">
        <div>
          <table class="bordered" style="width: 100%;">
            <thead>
              <tr>
                <th>Header Name</th>
                <th>Size</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="column in header" :key="column.key">
                <td><input v-model="column.name" /></td>
                <td><input v-model="column.size" /></td>
              </tr>
            </tbody>
          </table>
        </div>
        <div style="margin-top: 20px;">
          <button @click="showModal = false">Close</button>
        </div>
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
      header: [
        { name: 'Name', key: 'name', check: true, size: '150' },
        { name: 'Age', key: 'age', check: true, size: '50' },
        { name: 'Email', key: 'email', check: true, size: '200' },
        { name: 'Country', key: 'country', check: true, size: '100' },
        { name: 'Occupation', key: 'occupation', check: true, size: '150' }
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
  gap: 10px;
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

.edit {
  cursor: pointer;
  font-size: 13px;
  color: rgb(255, 136, 0);
}

.modal-content {
  width: 80%;
  max-width: 600px;
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
}
</style>

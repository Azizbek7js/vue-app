<template>
  <div class="main-container p-4">
    <input type="text" class="inputSearch" v-model="search" placeholder="Search...">
    <div class="table-container">
      <table class="bordered">
        <thead>
          <tr>
            <th v-for="column in displayedColumns" :key="column.name" :style="{ width: column.size < 1000 ? column.size + 'px': '1000px' }">{{ column.name }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in filteredData" :key="data.id">
            <td v-for="column in displayedColumns" :key="`${data.id}-${column.key}`" >{{ data[column.key] }}</td>
          </tr>
        </tbody>
      </table>
      <div class="checkbox-container">
        <div v-for="item in header" :key="item.name" class="checkbox-item">
          <input type="checkbox" v-model="item.check" />
          <i class="fas fa-pencil-alt edit" @click="openModal"></i>
          <p>{{ item.name }}</p>
        </div>
      </div>
    </div>
    <div class="input-container-1">
  <input
    type="text"
    v-model="formattedInputValue"
    @input="handleInput"
    placeholder="Enter number"
  />
</div>
    <div class="input-container-2">
  <input type="checkbox" v-model="inputCheck" />
  <input
    type="text"
    :class="{'inputCheckTrue': inputCheck, 'inputCheckFalse': !inputCheck}"
    placeholder="Enter number"
  />
</div>
    <div class="table-container-2">
      <table>
        <thead>
        <tr>
          <th rowspan="3">№</th>
          <th rowspan="3">Логотип</th>
          <th rowspan="3">Название</th>
          <th rowspan="3">СТИР</th>
          <th rowspan="3">Бириктирилган клиентлар</th>
          <th colspan="5">Контракт</th>
          <th colspan="6">Транкзации</th>
        </tr>
        <tr>
          <th colspan="2">Жами</th>
          <th colspan="3">Актив</th>
          <th colspan="2">Жами</th>
          <th colspan="2">Кабул килинди</th>
          <th rowspan="2">Фарки</th>
          <th rowspan="2">%</th>
        </tr>
        <tr>
          <th>Суммаси</th>
          <th>Сони</th>
          <th>Суммаси</th>
          <th>Сони</th>
          <th>Колдик суммаси</th>
          <th>Суммаси</th>
          <th>Сони</th>
          <th>Суммаси</th>
          <th>Сони</th>
        </tr>
        </thead>
      </table>
    </div>
    <div class="table-container-3">
      <table>
        <thead :class="{'head-top': !modalOpen }">
        <tr>
          <th  rowspan="2" :class="{'left': !modalOpen }">ФИО</th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">1</p>
            <p class="mb-0 caption">пн</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">2</p>
            <p class="mb-0 caption">вт</p>
          </th>
          <th  rowspan="3" >
            <p class="mb-0 caption font-weight-bold">3</p>
            <p class="mb-0 caption">ср</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold" >4</p>
            <p class="mb-0 caption">чт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">5</p>
            <p class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3" >
            <p  class="mb-0 caption font-weight-bold">6</p>
            <p class="mb-0 caption">сб</p>
          </th>
          <th rowspan="3" >
            <p class="mb-0 caption font-weight-bold">7</p>
            <p  class="mb-0 caption">вс</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">8</p>
            <p  class="mb-0 caption">пн</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">9</p>
            <p class="mb-0 caption">вт</p>
          </th>
          <th rowspan="3" >
            <p class="mb-0 caption font-weight-bold">10</p>
            <p data-v-679060de="" class="mb-0 caption">ср</p>
          </th>
          <th rowspan="3" class="">
            <p data-v-679060de="" class="mb-0 caption font-weight-bold">11</p>
            <p data-v-679060de="" class="mb-0 caption">чт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">12</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">13</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">14</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">15</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">16</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">17</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">18</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">19</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">20</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">21</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">22</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">23</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">24</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">25</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">26</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">27</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">28</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">29</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">30</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th rowspan="3">
            <p class="mb-0 caption font-weight-bold">31</p>
            <p data-v-679060de="" class="mb-0 caption">пт</p>
          </th>
          <th colspan="3" :class="{'right': !modalOpen }" >
          Итого
        </th>
        </tr>
        <tr>
          <th colspan="1" :class="{'right': !modalOpen }" style="right: 180px; top: 0; z-index: 9;">Лимит</th>
          <th colspan="1" :class="{'right': !modalOpen }"  style="right: 89px;top: 0; z-index: 9;">Собрано</th>
          <th colspan="1" :class="{'right': !modalOpen }"  style="right: 0;top: 0; z-index: 9;">Разница</th></tr>
        </thead>
        <tbody>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        <tr class="overall-row">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td>00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        </tbody>
      </table>
    </div>
    <div v-if="modalOpen" class="modal-container" @click.self="closeModal">
      <div class="modal-content">
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
  </div>
</template>

<script>
import draggable from 'vuedraggable';

export default {
  name: 'App',
  components: {
    draggable
  },
  data() {
    return {
      modalOpen: false,
      inputCheck: false,
      search: '',
      formattedInputValue : '',
      header: [
        { name: 'Name', key: 'name', check: true, size: 20 },
        { name: 'Age', key: 'age', check: true, size: 10 },
        { name: 'Email', key: 'email', check: true, size: 30 },
        { name: 'Country', key: 'country', check: true, size: 20 },
        { name: 'Occupation', key: 'occupation', check: true, size: 20 }
      ],
      tableData: [
        { id: 1, name: 'John Doe', age: 30, email: 'john@example.com', country: 'USA', occupation: 'Engineer' },
        { id: 2, name: 'Jane Smith', age: 25, email: 'jane@example.com', country: 'Canada', occupation: 'Doctor' },
        { id: 3, name: 'Bob Johnson', age: 35, email: 'bob@example.com', country: 'UK', occupation: 'Teacher' }
      ]
    }
  },
  watch: {
    header: {
      handler() {
        localStorage.setItem('header', JSON.stringify(this.header));
      },
      deep: true
    }
  },
  computed: {
    displayedColumns() {
      return this.header.filter(item => item.check);
    },
    filteredData() {
      const search = this.search.toLowerCase();
      return this.tableData.filter(item => {
        return Object.values(item).some(value =>
          String(value).toLowerCase().includes(search)
        );
      });
    }    
  },
  methods: {
    closeModal() {
      this.modalOpen = false;
    },
    handleInput(e) {
      this.formattedInputValue = this.numberFormatThree(e.target.value);
    },
    numberFormatThree(value) {
      if (!value) return '';
      let formattedValue = value.replace(/\s/g, "");
      formattedValue = formattedValue.replace(/\B(?=(\d{3})+(?!\d))/g, " ");
      return formattedValue;
    },
    openModal() {
      this.modalOpen = true;
    },
    handleKeydown(event) {
      if (event.key === 'Escape') {
        this.closeModal();
      }
      if(event.key === 'Enter') {
        this.closeModal();
      }
    }
  },
  mounted() {
    this.header = JSON.parse(localStorage.getItem('header')) || this.header;
    document.addEventListener('keydown', this.handleKeydown);
  },
  beforeDestroy() {
    document.removeEventListener('keydown', this.handleKeydown);
  }
}
</script>

<style>
.main-container{
  width: fit-content;
}
.table-container {
  max-width: 1920px;
  height: auto;
  display: flex;
  gap: 20px;
  margin-top: 20px; 
  text-align: center;
}
.table-container-2 {
  padding: 30px 0;
  table{
    width: 100%;
    background-color: #f5f5f5;
    border-collapse: collapse !important;
    border: 1px solid #e0e0e0;
    border-radius: 10px;
    thead {
      position: sticky;
      background-color: #f5f5f5 ;
      top: 0;
    }
    tr {
      position: relative;
      th {
        background-color: #f5f5f5;
        border-bottom: 1px solid #e0e0e0;
        border-right: 1px solid #e0e0e0;
        padding: 8px 16px;
        font-weight: 500;
        font-size: 14px;
        height: 20px;
        line-height: 20px;
      }
    }
  }
}
.table-container-3 {
  width: 1000px;
  height: 300px;
  overflow-y: auto;
  margin-bottom: 100px;
  .left{
    position: sticky;
    left: 0;
    z-index: 9;
  }
  .head-top{
    position: sticky;
    top: 0;
    left: 0;
    z-index: 10;
  }
  .right{
    position: sticky;
    right: 0;
    z-index: 9;
  }
  table{
    border-collapse: separate !important;
    border-spacing: 0;
    border-radius: 4px;
    white-space: nowrap;
    tbody {
        tr {
          td {
            background-color: #ffffff !important;
            border: 1px solid #ececec;
            padding: 8px 16px;
            text-align: center !important;
            font-weight: 500;
            font-size: 14px;
            line-height: 20px;
            color: #000000;
          }

          &:hover {
            td {
              background-color: aliceblue;
            }
          }
        }
      }
    tr {
      th {
        background-color: #f5f5f5 !important;
        border: 1px solid #ececec;
        padding: 8px 16px;
        text-align: center !important;
        font-weight: 500;
        font-size: 14px;
        line-height: 20px;
        color: #000000;
      }
    }
  }
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

.edit {
  cursor: pointer;
  font-size: 13px;
  color: rgb(255, 136, 0);
}
.input-container-1 {
  position: relative;
  width: 300px;
  margin: 30px 0;
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

.input-container-1 input {
  width: 100%;
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.input-container-1 input:focus {
  border-color: #007BFF;
  box-shadow: 0 0 8px rgba(0, 123, 255, 0.2);
  outline: none;
}
.input-container-2 {
  display: flex;
  align-items: center;
  gap: 30px;
  width: 300px;
  margin: 30px 0;
}
.inputCheckFalse{
  width: 100%;
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}
.inputCheckTrue{
  width: 100%;
  padding: 10px;
  border-radius: 4px;
  font-size: 16px;
  border-color: #007BFF;
  color: #007BFF ;
  outline: none;
}

</style>
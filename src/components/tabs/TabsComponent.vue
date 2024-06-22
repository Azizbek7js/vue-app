<template>
  <div>
    <div class="tabs-container">
      <div class="w-25 h-100 d-flex align-items-center justify-content-center" :class="{'border-bottom': tab === 0}" @click="tab = 0" style="cursor: pointer; color: white">table-1</div>
      <div class="w-25 h-100 d-flex align-items-center justify-content-center" :class="{'border-bottom': tab === 1}" @click="tab = 1" style="cursor: pointer; color: white">table-2</div>
    </div>
    <div v-if="tab === 0" class="table-container-2">
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
    <div v-else class="table-container-3">
      <table>
        <thead :class="{'head-top': !modalOpen }">
        <tr>
          <th  rowspan="2" :class="{'left': !modalOpen }">ФИО</th>
          <th rowspan="3" v-for="index in 31" :key="index">
            <p class="mb-0 caption font-weight-bold">{{index}}</p>
            <p class="mb-0 caption">пн</p>
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
        <tr class="overall-row" v-for="t in 10" :key="t">
          <td :class="{'left': !modalOpen }">SALARYMETHOD</td>
          <td v-for="index in 31" :key="index">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:180px;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right:89px ;top: 0;">00:00</td>
          <td :class="{'right': !modalOpen }" style="right: 0;top: 0;">00:00</td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name:'TabsComponent',
  data(){
    return{
      tab: 0,
    }
  },
  methods: {

  }
}
</script>

<style scoped>
.tabs-container{
  margin-left: 300px;
  margin-bottom: 10px;
  width: 500px;
  height: 50px;
  background-color: #007BFF;
  display: flex;
  align-items: center;
  justify-content: center;
}
.table-container-2 {
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
  height: 400px;
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

</style>

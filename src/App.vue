<template>
  <div class="viewport">
    <div class="sidebar">
      <header>
        <a @click="route = 'main'">My App</a>
      </header>
      <ul class="box">
        <li @click="route = 'table'" class="rounded mt-2" :class="{'bg-primary':route==='table'}">
          <a>
            <i class="fas fa-1"></i> Table
          </a>
        </li>
        <li @click="route = 'input'" class="rounded" :class="{'bg-primary':route==='input'}">
          <a>
            <i class="fas fa-2"></i> Input
          </a>
        </li>
        <li @click="route = 'tabs'" class="rounded" :class="{'bg-primary':route==='tabs'}">
          <a>
            <i class="fas fa-3"></i> Tabs
          </a>
        </li>
        <li @click="route = 'panel'" class="rounded" :class="{'bg-primary':route==='panel'}">
          <a>
            <i class="fas fa-4"></i>Panel
          </a>
        </li>
      </ul>
    </div>
    <div class="content">
      <div class="main-container">
          <div v-if="route==='table'">
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
                    <td v-for="column in displayedColumns" :key="`${data.id}-${column.key}`" >{{ data[column.key] }}</td>
                  </tr>
                  </tbody>
                </table>
                <div class=" d-flex align-items-center justify-content-end p-2">
                  <button class="btn border rounded mx-1" v-for="pageNumber in pages" @click="page = pageNumber" :class="{'btn-primary':pageNumber === page}"  :key="pageNumber"> {{pageNumber}} </button>
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
          </div>
          <div v-if="route==='input'">
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
          </div>
          <div v-if="route === 'tabs'">
            <div class="tabs-container">
              <div class="w-25 h-100 d-flex align-items-center justify-content-center " :class="{'border-bottom': tab===0}" @click="tab = 0" style="cursor: pointer ; color: white">
                table-1
              </div>
              <div class="w-25 h-100 d-flex align-items-center justify-content-center" :class="{'border-bottom': tab===1}" @click="tab = 1" style="cursor: pointer; color: white" >
                table-2
              </div>
            </div>
            <div v-if="tab===0" class="table-container-2">
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
          </div>
          <div v-if="route==='panel'" class="pt-4" style="height: 400px;">
            <input type="checkbox" v-model="allShowItems" >
            <div class="category border rounded px-4 py-2" v-for="item in itemsComputed" :key="item.name" :class="{'my-3': item.isOpen === true}">
              <div class="d-flex align-items-center justify-content-between" @click="toogleOpen(item)">
                <span>{{item.name}}</span>
                <i :class="{'fas fa-chevron-down small': item.isOpen=== false ,'fas fa-chevron-up small': item.isOpen=== true}" ></i>
              </div>
              <p class="pt-2" v-if="item.isOpen">{{item.text}}</p>
            </div>
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
      tab: 0,
      route: 'main',
      status:'ALL',
      modalOpen: false,
      inputCheck: false,
      search: '',
      formattedInputValue : '',
      page: 1,
      perPage: 5,
      pages: [],
      showBottom:false,
      items:[
        {name: 'item-1' , isOpen: false , text:'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat' },
        {name: 'item-2' , isOpen: false , text:'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat' },
        {name: 'item-3' , isOpen: false , text:'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat' },
        {name: 'item-4' , isOpen: false , text:'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat' }
      ],
      allShowItems:false,
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
      ]
    }
  },
  watch: {
    header: {
      handler() {
        localStorage.setItem('header', JSON.stringify(this.header));
      },
      deep: true
    },
    posts () {
      this.setPages();
    },
    allShowItems(val){
      if(val){
        this.items.map(item => item.isOpen = true)
      }else {
        this.items.map(item => item.isOpen = false)
      }
    }
  },
  computed: {
    itemsComputed(){
      return this.items
    },
    displayedColumns() {
      return this.header.filter(item => item.check );
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
    setPages () {
      let numberOfPages = Math.ceil(this.tableData.length / this.perPage);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    toogleOpen(item){
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
      console.log(this.items)
    },
    changeStatus(status){
      this.status = status
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
    this.setPages()
    this.header = JSON.parse(localStorage.getItem('header')) || this.header;
    document.addEventListener('keydown', this.handleKeydown);
  },
  beforeDestroy() {
    document.removeEventListener('keydown', this.handleKeydown);
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
.category{
  width: 600px;
  transition: all 0.25s;
}
.table-container {
  max-width: 1920px;
  height: auto;
  display: flex;
  gap: 20px;
  margin-top: 20px;
  text-align: center;
}
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
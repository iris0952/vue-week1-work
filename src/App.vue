<script setup>
import { ref } from 'vue'

const menuData = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    quantity: 20
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    quantity: 18
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    quantity: 34
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    quantity: 10
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    quantity: 25
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    quantity: 20
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    quantity: 18
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    quantity: 20
  }
])

const tempData = ref({
  id: 0,
  name: '',
  description: '',
  price: 0,
  quantity: 0
})
const editMenu = (menu) => {
  tempData.value = { ...menu }
  console.log(tempData.value)
}
const confirmEdit = () => {
  const index = menuData.value.findIndex((item) => item.id === tempData.value.id)
  menuData.value[index] = tempData.value
  tempData.value = {
    id: 0,
    name: '',
    description: '',
    price: 0,
    quantity: 0
  }
}
const addQty = (menu) => {
  menu.quantity += 1
}
const minusQty = (menu) => {
  if (menu.quantity > 0) {
    menu.quantity -= 1
    console.log('click -1')
  } else {
    menu.quantity = 0
  }
}
</script>

<template>
  <div class="container">
    <table>
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="menu in menuData" :key="menu.id">
          <td>{{ menu.name }}</td>
          <td>
            <small>{{ menu.description }}</small>
          </td>
          <td>{{ menu.price }}</td>
          <td>
            <button type="button" @click="minusQty(menu)">-</button>
            <span class="num">{{ menu.quantity }}</span>
            <button type="button" @click="addQty(menu)">+</button>
          </td>
          <td><button type="button" @click="editMenu(menu)">編輯</button></td>
        </tr>
      </tbody>
    </table>
    <hr />
    <div class="editArea">
      <h2>修改商品資訊</h2>
      <div class="inputArea">
        <label for="name">品項：{{ tempData.name }} </label>
        <input id="name" type="text" v-model="tempData.name" />
      </div>
      <div class="inputArea">
        <label for="description">描述：{{ tempData.description }} </label>
        <input id="description" type="text" v-model="tempData.description" />
      </div>
      <div class="inputArea">
        <label for="price">價格：{{ tempData.price }} 元</label>
        <input id="price" type="text" v-model="tempData.price" />
      </div>
      <div class="inputArea">
        <label for="quantity">庫存：{{ tempData.quantity }} 個</label>
        <input id="quantity" type="text" v-model="tempData.quantity" />
      </div>
      <button type="button" @click="confirmEdit(menu)" class="me-3">儲存編輯</button>
      <button type="button" @click="tempData = {}">取消編輯</button>
    </div>
  </div>
</template>

<style scoped>
th {
  font-size: 1.2rem;
}
label {
  margin-right: 5px;
}
.inputArea {
  margin-bottom: 5px;
}
.me-3 {
  margin-right: 5px;
}
.num {
  display: inline-block;
  width: 50px;
  text-align: center;
}
</style>

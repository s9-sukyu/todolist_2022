<script setup>
import { ref } from "vue";

const items = ref([
  { name: "線形代数", priority: 100 },
  { name: "おひるね", priority: 52 },
  { name: "あああ", priority: 532 },
]);
const items_done = ref([
  { name: "線形代数", priority: 100 },
  { name: "おひるね", priority: 5 },
]);
const newItemName = ref("");
const newItemPrice = ref(0);

const addItem = () => {
  items.value.push({ name: newItemName.value, priority: newItemPrice.value });
};
const deleteItem = (item, index) => {
  items_done.value.push(item);
  items.value.splice(index, 1);
};
</script>

<template>
  <div>
    <div>現在のタスク</div>
    <table rules="rows">
      <thead>
        <tr>
          <th>名前</th>
          <th>優先度</th>
          <th>おわり</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="item.name">
          <td class="name">{{ item.name }}</td>
          <td class="price">{{ item.priority }}</td>
          <td>
            <button @click="deleteItem(item, index)">　</button>
          </td>
          <div v-if="item.price >= 10000">高額商品</div>
        </tr>
      </tbody>
    </table>

    <div>
      <label>
        名前
        <input v-model="newItemName" type="text" />
      </label>
      <label>
        優先度
        <input v-model="newItemPrice" style="width: 50px" type="number" />
      </label>
      <button @click="addItem">add</button>
    </div>

    <div>終了したタスク</div>
    <table rules="rows">
      <thead>
        <tr>
          <th>名前</th>
          <th>優先度</th>
          <th>取り除く</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items_done" :key="item.priority">
          <td class="name">{{ item.name }}</td>
          <td class="price">{{ item.priority }}</td>
          <td><button @click="items_done.splice(index, 1)">　</button></td>
          <div v-if="item.price >= 10000">高額商品</div>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
.over500 {
  color: red;
}
table {
  margin: auto;
}
th {
  padding: 10px;
  background-color: #eeeeee;
}
td {
  padding: 10px;
}
</style>

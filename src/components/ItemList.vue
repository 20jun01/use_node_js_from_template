<script setup>
import { ref } from "vue";

const items = ref([
  { name: "たまご", price: 100 },
  { name: "りんご", price: 160 },
]);
const newItemName = ref("");
const newItemPrice = ref(0);
const addItem = () => {
  if (!(newItemName.value == "" || newItemPrice.value == 0)) {
    items.value.push({ name: newItemName.value, price: newItemPrice.value });
  }
  newItemName.value = "";
  newItemPrice.value = 0;
};

const todos = ref([]);
const newTodoName = ref("");
const newTodoPrim = ref(0);
const addTodo = () => {
  if (!(newTodoName.value == "" || newTodoPrim.value == 0)) {
    todos.value.push({
      name: newTodoName.value,
      prim: newTodoPrim.value,
      isDone: false,
    });
  }
  newTodoName.value = "";
  newTodoPrim.value = 0;
};
</script>

<template>
  <div>ItemList</div>
  <div v-for="item in items" :key="item.name">
    <div class="item" :class="{ over500: item.price >= 500 }">
      <div class="name">名前: {{ item.name }}</div>
      <div class="price">{{ item.price }} 円</div>
      <div v-if="item.price >= 10000">高額商品</div>
    </div>
  </div>
  <div>
    <label>
      名前
      <input v-model="newItemName" type="text" />
    </label>
    <label>
      価格
      <input v-model="newItemPrice" type="number" />
    </label>
    <button @click="addItem">add</button>
  </div>

  <div>TodoList</div>
  <div v-for="todo in todos" :key="todo.name">
    <div class="todo">
      <div v-if="todo.isDone == false" class="name">
        すること: {{ todo.name }}
      </div>
      <div v-if="todo.isDone == false" class="prim">
        優先度: {{ todo.prim }}
      </div>
      <button v-if="todo.isDone == false" @click="todo.isDone = true">
        完了
      </button>
    </div>
  </div>
  <div>DoneList</div>
  <div v-for="todo in todos" :key="todo.name">
    <div class="done">
      <div v-if="todo.isDone == true" class="name">
        したこと: {{ todo.name }}
      </div>
      <button v-if="todo.isDone == true" @click="todo.isDone = false">
        やっぱ嘘
      </button>
    </div>
  </div>
  <div>
    <label>
      タイトル
      <input v-model="newTodoName" type="text" />
    </label>
    <label>
      優先度
      <input v-model="newTodoPrim" type="number" />
    </label>
    <button @click="addTodo">追加</button>
  </div>
</template>

<style>
.over500 {
  color: red;
}
</style>

<script setup>
// import { RouterLink, RouterView } from "vue-router";
// import HelloWorld from "./components/HelloWorld.vue";
import { ref } from 'vue';

let newItem = ref('');
let itemList = ref([]);
let updatedItem = ref('');

function addItem() {
  itemList.value.push({
    status: false,
    content: newItem.value,
    edit: false,
  });

  newItem.value = '';
}

function complete(item) {
  item.status = !item.status;
}

function edit(item) {
  item.edit = true;
  updatedItem = item.content;
}

function update(item, event) {
  item.content = event.target.value;
  item.edit = false;
}

function remove(index) {
  itemList.value.splice(index, 1);
}
</script>

<template>
<div class="todoApp">
  <h1>To do app</h1>
  <form action="" @submit.prevent="addItem()">
    <input type="text" placeholder="Add new to do item here" v-model="newItem">
    <button>Add new</button>
  </form>
  <ul v-for="(item, index) in itemList">
    <li><span class="item" :class="{ doneChecked : item.status }" :id="index">{{item.content}}</span><span class="edit" @click="edit(item)">Edit</span><span class="done" @click="complete(item)">Done</span><span class="delete" @click="remove(index)">Delete</span>
    <input type="text" @keyup.enter="update(item, $event)" :class="{ editShow : item.edit }" v-text="updatedItem" :value="item.content"></li>
  </ul>
</div>
</template>

<style scoped>
.todoApp {
  margin: 0 auto;
  width: fit-content;
}

ul {
  margin: 0 auto;
}

li {
  position: relative;
  width: 500px;
  margin-bottom: 50px;
}

li span.edit,
li span.done,
li span.delete {
  position: absolute;
  top: 0;
  left: 100%;
  cursor: pointer;
}

li span.done {
  left: 110%;
}

li span.delete {
  left: 120%;
}

li input {
  position: absolute;
  top: 100%;
  left: 0;
  display: none;
}

li input.editShow {
  display: block;
}

.doneChecked {
  text-decoration: line-through;
}
</style>

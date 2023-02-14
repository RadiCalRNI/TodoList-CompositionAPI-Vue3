<template>
  <app-header></app-header>
  <main>
    <add-todo @addTodo="addNewTodo"></add-todo>

    <ul class="todos">
      <todo-item
        v-for="(task, index) in list"
        :key="task.key"
        :todo="task"
        @delete="deleteTodo"
        @checked="checked"
        @dragover.prevent
        @dragstart="dragStart(index)"
        @drop="dragEnd(index)"
      ></todo-item>
    </ul>

    <app-stat
      @deleteCompleted="deleteCompleted"
      :counter="unCheckedTask"
      @activeTab="getTodo"
    ></app-stat>
  </main>
  <app-footer></app-footer>
</template>

<script setup>
import AppHeader from "./components/AppHeader.vue";
import AddTodo from "./components/AddTodo.vue";
import TodoItem from "./components/TodoItem.vue";
import AppFooter from "./components/AppFooter.vue";
import AppStat from "./components/AppStat.vue";
import { computed, ref } from "vue";

const todoList = ref([]);
const dragging = ref(-1);
const tab = ref("");

function addNewTodo(title) {
  if (title) {
    const key = Math.random().toString(16).slice(2);
    const isComplete = false;
    const task = { key, title, isComplete };
    todoList.value.push(task);
  }
}

function deleteTodo(key) {
  todoList.value = todoList.value.filter((item) => item.key != key);
}

function checked(key, isComplete) {
  todoList.value.forEach((item) => {
    if (item.key == key) {
      item.isComplete = isComplete;
    }
  });
}

function deleteCompleted() {
  todoList.value = todoList.value.filter((item) => item.isComplete === false);
}

function dragStart(index) {
  dragging.value = index;
}

function dragEnd(index) {
  const element = todoList.value.splice(dragging.value, 1)[0];
  todoList.value.splice(index, 0, element);
}

function getTodo(activeTab) {
  tab.value = activeTab;
}

const unCheckedTask = computed(() => {
  let unCheckedTasks = todoList.value.filter(
    (item) => item.isComplete == false
  );
  return unCheckedTasks.length;
});

const list = computed(() => {
  if (tab.value == "all") {
    return todoList.value;
  } else if (tab.value == "active") {
    return todoList.value.filter((item) => item.isComplete === false);
  } else if (tab.value == "completed") {
    return todoList.value.filter((item) => item.isComplete === true);
  } else {
    return todoList.value;
  }
});
</script>

<style></style>

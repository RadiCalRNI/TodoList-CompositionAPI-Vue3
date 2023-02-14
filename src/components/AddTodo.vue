<template>
  <div class="card add">
    <div class="cb-container">
      <button id="add-btn" @click="addTodo">+</button>
    </div>
    <div class="txt-container">
      <label for="addt">افزودن </label>
      <input
        type="text"
        class="txt-input"
        placeholder="افزودن وظیفه جدید..."
        spellcheck="false"
        autocomplete="off"
        id="addt"
        dir="rtl"
        v-model="todoText"
        @keypress.enter="addTodo"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const todoText = ref("");

const emit = defineEmits(["addTodo"])
function addTodo() {
  emit("addTodo", todoText.value);
  todoText.value = "";
}
</script>

<style></style>

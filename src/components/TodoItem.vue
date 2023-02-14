<template>
  <li class="card" draggable="true">
    <div class="cb-container">
      <input
        type="checkbox"
        class="cb-input"
        :checked="props.todo.isComplete ? true : false"
        @click="checked"
      />
      <span class="check"></span>
    </div>
    <p class="item">
      <del v-if="props.todo.isComplete">{{ props.todo.title }}</del>
      <span v-else v-text="props.todo.title"></span>
    </p>
    <button class="clear" @click="deleteTodo">
      <img src="../assets/images/icon-cross.svg" alt="Clear it" />
    </button>
  </li>
</template>

<script setup>
import { defineEmits, defineProps } from "vue";

const props = defineProps({ todo: Object });
const emits = defineEmits(["delete", "checked"]);

const deleteTodo = () => {
  if (confirm("آیا از حذف تسک مطعمن هستید؟")) {
    emits("delete", props.todo.key);
  }
};

const checked = () => {
  emits("checked", props.todo.key, !props.todo.isComplete);
};
</script>

<style></style>

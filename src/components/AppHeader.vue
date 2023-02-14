<template>
  <header class="card">
    <h1>لیست وظایف</h1>
    <button id="theme-switcher" @click="changeTheme">
      <img
        v-if="defaultTheme == 'dark'"
        src="../assets/images/icon-sun.svg"
        alt="Change color theme"
      />
      <img
        v-else
        src="../assets/images/icon-moon.svg"
        alt="Change color theme"
      />
    </button>
  </header>
</template>

<script setup>
import { ref } from "vue";
const defaultTheme = ref("dark");
function changeTheme() {
  if (defaultTheme.value == "dark") {
    defaultTheme.value = "light";
    document.body.classList.add("light");
  } else {
    defaultTheme.value = "dark";
    document.body.classList.remove("light");
  }
}
</script>

<style></style>

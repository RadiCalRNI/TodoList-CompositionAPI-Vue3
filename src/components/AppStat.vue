<template>
  <div class="card stat">
    <p class="corner">
      <span id="items-left">{{ props.counter }}</span> مورد باقی مانده
    </p>
    <div class="filter">
      <button
        id="all"
        :class="{ on: activeTab === 'all' }"
        @click="changeTab('all')"
      >
        همه
      </button>
      <button
        id="active"
        :class="{ on: activeTab === 'active' }"
        @click="changeTab('active')"
      >
        فعال
      </button>
      <button
        id="completed"
        :class="{ on: activeTab === 'completed' }"
        @click="changeTab('completed')"
      >
        تکمیل
      </button>
    </div>
    <div class="corner">
      <button id="clear-completed" @click="deleteCompleted">
        حذف تکمیل شده ها
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from "vue";
const activeTab = ref("all");
const props = defineProps({ counter: Number });
const emits = defineEmits(["deleteCompleted", "activeTab"]);

function deleteCompleted() {
  if (confirm("آیا از حذف تسک های انجام شده اطمینان دارید؟")) {
    emits("deleteCompleted");
  }
}

function changeTab(status) {
  activeTab.value = status;
  emits("activeTab", activeTab.value);
}
</script>

<style></style>

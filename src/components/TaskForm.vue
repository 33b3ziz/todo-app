<script lang="ts" setup>
import { ref } from "vue";

const emit = defineEmits<{
  addTask: [newTask: string];
}>();

const newTask = ref("");
const error = ref("");

const formSubmitted = () => {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim());
    newTask.value = "";
  } else {
    error.value = "Task cannot be empty";
  }
};
</script>

<template>
  <form @submit.prevent="formSubmitted">
    <label>
      New Task
      <input
        type="text"
        name="newTask"
        v-model="newTask"
        :aria-invalid="!!error || undefined"
        @input="error = ''"
      />
      <small id="invalid-helper">{{ error }}</small>
    </label>
    <div class="button-container">
      <button>Add</button>
    </div>
  </form>
</template>

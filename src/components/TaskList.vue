<script lang="ts" setup>
import type { Task } from "../types";

const props = defineProps<{
  tasks: Task[];
}>();

const emits = defineEmits<{
  toggleDone: [id: string];
  deleteTask: [id: string];
}>();
</script>

<template>
  <TransitionGroup name="task-list" tag="div" class="task-list">
    <article v-for="task in props.tasks" :key="task.id" class="task">
      <label>
        <input
          type="checkbox"
          @input="emits('toggleDone', task.id)"
          :checked="task.done"
        />
        <span :class="{ done: task.done }">
          {{ task.title }}
        </span>
      </label>
      <button @click="emits('deleteTask', task.id)" class="outline">
        Delete
      </button>
    </article>
  </TransitionGroup>
</template>

<style>
.task-list {
  margin-top: 1rem;
}

.done {
  text-decoration: line-through;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-list-enter-active,
.task-list-leave-active {
  transition: all 0.5s ease;
}

.task-list-enter-from,
.task-list-leave-to {
  opacity: 0;
  transform: translateX(300px);
}
</style>

<template>
  <div class="list">
    <div
      class="item"
      v-bind:class="{ done: task.done }"
      v-for="task in tasks"
      :key="task.text"
    >
      <input type="checkbox" v-model="task.done" />
      {{ task.text }}<like v-model="task.likes"/>
    </div>
  </div>
</template>

<script>
import Like from './Like.vue';

export default {
    props: ['task', 'tasks'],
    components: {
        Like
    }
}
</script>

<style>
</style>
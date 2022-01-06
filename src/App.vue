<template>
<div>
  <h1>Список задач<like v-model="headerLikes"/></h1>
  <h3>Количество лайков - {{ countLikes }}</h3>
  <div v-if="count == 0">Вы великолепны!</div>
  <div v-else-if="count == 1">Осталя последний рывок!</div>
  <div v-else>
    Осталось сделать задач: <span class="counter">{{ count }}</span>
  </div>

  
  <tasks :task="this.tasks" :tasks="uncompletedTasks"/>
  <div class="form">
    <input v-model="textTask" />
    <input type="submit" value="Добавить" @click="addTask" /><like v-model="formLikes"/>
  </div>
  <transition name="bounce">
    <img src="rob.jpg" alt="#" v-show="count == 0" />
  </transition>

  <tasks :task="this.tasks" :tasks="completeTasks"/>
  </div>
</template>

<script>
import Tasks from './components/Tasks.vue';
import Like from './components/Like.vue';

export default {
  name: "App",
  data() {
    return {
      headerLikes: 2,
      formLikes: 3,
      textTask: "",
      nameForTask: "Название задачи",
      tasks: [
        { text: "Развернуть окружение в Codepen", done: true, likes: 0 },
        { text: "Пройти курс по Vue", done: false, likes: 3 },
        { text: "Сделать интернет-магазин на Vue", done: false, likes: 5 },
      ],
    };
  },
  methods: {
    addTask() {
      this.tasks.push({ text: this.textTask, done: false, likes: 0 });
      this.textTask = "";
    },
    
  },
  computed: {
    count() {
      return this.tasks.filter((task) => !task.done).length;
    },
    completeTasks() {
      return this.tasks.filter((task) => task.done);
    },
    uncompletedTasks() {
      return this.tasks.filter((task) => !task.done);
    },
    countLikes() {
      return this.headerLikes + this.formLikes + this.tasks.reduce((value, task) => value + task.likes, 0);
    }
  },
  components: {
    Tasks,
    Like
  }
};


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<template>
  <div id="app">
    <section class="students_list">
      <student-card
        v-for="student in students"
        :key="student.id"
        :students_data="student"
      ></student-card>
    </section>
  </div>
</template>

<script>
import StudentCard from "@/components/StudentCard.vue";
export default {
  name: "App",
  components: {
    StudentCard,
  },

  data() {
    return {
      students: null,
      // student: {},
    };
  },
  async mounted() {
    const url = "https://api.hatchways.io/assessment/students";
    const response = await fetch(url);
    const data = await response.json();
    this.students = data.students;
  },
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

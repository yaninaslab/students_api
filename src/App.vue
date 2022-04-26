<template>
  <div id="app">
    <input
      class="search-input"
      v-model="search"
      type="text"
      placeholder="Search by name"
    />
    <input
      class="search-input"
      v-model="searchtag"
      type="text"
      placeholder="Search by tag"
    />
    <section class="students-list">
      <student-card
        v-for="student in filteredStudents"
        :key="student.id"
        :studentsData="student"
        :addTag="addTag"
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
      students: [],
      search: "",
      searchtag: "",
    };
  },
  async created() {
    const url = "https://api.hatchways.io/assessment/students";
    const response = await fetch(url);
    const data = await response.json();
    this.students = data.students.map((student) => ({ ...student, tags: [] }));
  },
  methods: {
    addTag(studentId, tagName) {
      const currentStudent = this.students.find(
        (student) => student.id === studentId
      );

      if (currentStudent) {
        currentStudent.tags.push(tagName);
      }
    },
  },
  computed: {
    filteredStudents() {
      return this.students.filter((student) =>
        student.firstName
          .concat(student.lastName)
          .toLowerCase()
          .includes(this.search)
      );
    },
  },
};
</script>

<style>
.students-list {
  display: grid;
  margin-top: 60px;
}
.search-input {
  margin: 10px;
  border: 0.7px solid lightgrey;
  border-top-style: hidden;
  border-right-style: hidden;
  border-left-style: hidden;
  border-bottom-style: ridge;
  width: 100%;
  height: 30px;
}
#app {
  font-family: "Montserrat", sans-serif;
  font-family: "Raleway", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

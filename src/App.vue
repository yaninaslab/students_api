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
      <!-- <tags-input :addTag="addTag"></tags-input> -->
    </section>
  </div>
</template>

<script>
import StudentCard from "@/components/StudentCard.vue";
// import TagsInput from "@/components/TagsInput.vue";
export default {
  name: "App",
  components: {
    StudentCard,
    // TagsInput,
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
      console.log(currentStudent);

      if (currentStudent) {
        currentStudent.tags.push(tagName);
      }
    },
  },
  computed: {
    filteredStudents() {
      let filterByName = this.students.filter((student) =>
        student.firstName
          .concat(student.lastName)
          .toLowerCase()
          .includes(this.search)
      );
      if (!this.searchtag) {
        return filterByName;
      }
      return filterByName.filter((student) =>
        student.tags.find((tag) => tag.includes(this.searchtag))
      );
    },
  },
};
</script>

<style>
.students-list {
  display: grid;
  max-width: 600px;
  margin: 60px auto 0;
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
input:focus {
  outline: none;
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

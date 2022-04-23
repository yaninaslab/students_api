<template>
  <div>
    <article class="user_card">
      <img :src="students_data.pic" />
      <h3>{{ students_data.firstName }} {{ students_data.lastName }}</h3>
      <p>Email: {{ students_data.email }}</p>
      <p>Company: {{ students_data.company }}</p>
      <p>Skill: {{ students_data.skill }}</p>
      <p>Average: {{ students_data.grades }}</p>
    </article>
  </div>
</template>

<script>
export default {
  name: "student-card",
  props: {
    students_data: {
      type: Object,
      default() {
        return {};
      },
    },
  },
};
</script>

<style scoped></style>

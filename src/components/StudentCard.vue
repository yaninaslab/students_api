<template>
  <article class="user-card">
    <img class="student-pic" :src="studentsData.pic" />
    <div class="student-info">
      <h1 class="student-name">
        {{ studentsData.firstName }} {{ studentsData.lastName }}
      </h1>
      <p>Email: {{ studentsData.email }}</p>
      <p>Company: {{ studentsData.company }}</p>
      <p>Skill: {{ studentsData.skill }}</p>
      <p>Average: {{ calcAverage(studentsData.grades) }}%</p>
      <div class="tag" v-for="(tag, index) in tags" :key="'tag' + index">
        <span>{{ tag }}</span>
      </div>
      <input
        v-model="tagValue"
        @keyup.enter="addTags"
        class="tags-input"
        type="text"
      />
      <div class="test-results" v-if="resultsOpened">
        <p>Test 1: &nbsp;&nbsp;&nbsp;&nbsp; {{ studentsData.grades[0] }}%</p>
        <p>Test 2: &nbsp;&nbsp;&nbsp;&nbsp; {{ studentsData.grades[1] }}%</p>
        <p>Test 3: &nbsp;&nbsp;&nbsp;&nbsp; {{ studentsData.grades[2] }}%</p>
        <p>Test 4: &nbsp;&nbsp;&nbsp;&nbsp; {{ studentsData.grades[3] }}%</p>
        <p>Test 5: &nbsp;&nbsp;&nbsp;&nbsp; {{ studentsData.grades[4] }}%</p>
        <p>Test 6: &nbsp;&nbsp;&nbsp;&nbsp; {{ studentsData.grades[5] }}%</p>
        <p>Test 7: &nbsp;&nbsp;&nbsp;&nbsp; {{ studentsData.grades[6] }}%</p>
        <p>Test 8: &nbsp;&nbsp;&nbsp;&nbsp; {{ studentsData.grades[7] }}%</p>
      </div>
    </div>
    <div class="expand">
      <button @click="openResults" class="add-btn" v-if="expand">+</button>
      <button @click="openResults" class="add-btn" v-else>-</button>
    </div>
  </article>
</template>

<script>
export default {
  name: "student-card",
  data() {
    return {
      resultsOpened: false,
      expand: true,
      tagValue: "",
      tags: [],
    };
  },
  methods: {
    calcAverage(grades) {
      const average =
        grades.reduce((acc, grade) => {
          return acc + Number(grade);
        }, 0) / grades.length;
      return average;
    },
    openResults() {
      if (this.resultsOpened === false && this.expand === true) {
        this.resultsOpened = true;
        this.expand = false;
      } else {
        this.resultsOpened = false;
        this.expand = true;
      }
    },
    addTags() {
      if (!this.tagValue == "") {
        this.tags.push(this.tagValue);
        this.tagValue = "";
      }
    },
  },
  props: {
    studentsData: {
      type: Object,
    },
    addTag: {
      type: Function,
    },
  },
};
</script>

<style scoped>
.user-card {
  display: flex;
  justify-content: center;
  grid-auto-flow: column;
  column-gap: 100px;
  border: 0.7px solid lightgrey;
  max-width: 100%;
  border-top-style: hidden;
  border-right-style: hidden;
  border-left-style: hidden;
  padding-bottom: 10px;
}
p {
  margin: 0;
  padding: 0;
}
.student-pic {
  width: 100px;
  height: 100px;
  border: black 1px;
}
img {
  border-radius: 5 px 5px 20px 5px;
  border-radius: 50%;
  background: whitesmoke;
  border: black;
}
.student-name {
  text-transform: uppercase;
  font-size: xx-large;
  font-weight: bolder;
}
.add-btn {
  height: 30px;
  width: 30px;
  font-size: xx-large;
  color: grey;
  background-color: white;
  border: none;
  cursor: pointer;
}
.test-results {
  margin: 10px;
}
.tags-input {
  margin: 10px;
  border: 0.7px solid lightgrey;
  border-top-style: hidden;
  border-right-style: hidden;
  border-left-style: hidden;
  border-bottom-style: ridge;
  width: 100%;
  height: 30px;
}
.tag {
  float: left;
  margin-top: 10px;
  padding: 3px 5px;
}
span {
  background-color: lightgray;
  padding: 5px 10px;
  border-radius: 5px;
  color: black;
}
</style>

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
      <div
        class="tag"
        v-for="(tag, index) in studentsData.tags"
        :key="'tag' + index"
      >
        <span class="tags">{{ tag }}</span>
      </div>
      <input
        v-model="tagValue"
        @keyup.enter="addTags"
        class="tags-input"
        type="text"
      />
      <div class="test-results" v-if="resultsOpened">
        <div
          v-for="(grade, index) in studentsData.grades"
          :key="'grade' + index"
        >
          <p class="results">
            <span class="margin">Test {{ index + 1 }}:</span>{{ grade }}%
          </p>
        </div>
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
        this.addTag(this.studentsData.id, this.tagValue);
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
  padding-top: 10px;
  display: flex;
  justify-content: space-between;
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
  border-radius: 50%;
  border: 1px solid lightgray;
  width: 100px;
  height: 100px;
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
.tags {
  background-color: lightgray;
  padding: 5px 10px;
  border-radius: 5px;
  color: black;
}
.margin {
  margin-right: 20px;
}
.results {
  display: flex;
  justify-content: center;
}
</style>

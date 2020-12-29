<template>
  <div class="home">
    <h2>{{ student.first_name }} {{ student.last_name }}</h2>
    <h4>{{ student.email }}</h4>
    <h4>{{ student.phone_number }}</h4>
    <h4>{{ student.short_bio }}</h4>
    <h4>{{ student.linkedin_url }}</h4>
    <h4>{{ student.twitter_handle }}</h4>
    <h4>{{ student.personal_website_url }}</h4>
    <h4>{{ student.online_resume_url }}</h4>
    <h4>{{ student.github_url }}</h4>
    <img v-bind:src="student.photo_url">

    <h3>Experience:</h3>
    <div v-for="experience in student.experiences">
      <h4>{{ experience.start_date }}</h4>
      <h4>{{ experience.end_date }}</h4>
      <h4>{{ experience.job_title }}</h4>
      <h4>{{ experience.company_name }}</h4>
      <h4>{{ experience.details }}</h4>
    </div>

    <h3>Education:</h3>
    <div v-for="education in student.educations">
      <h4>{{ education.start_date }}</h4>
      <h4>{{ education.end_date }}</h4>
      <h4>{{ education.degree }}</h4>
      <h4>{{ education.university_name }}</h4>
      <h4>{{ education.details }}</h4>
    </div>

    <h3>Skills:</h3>
    <div v-for="skill in student.skills">
      <h4>{{ skill.name }}</h4>
    </div>

    <h3>Capstone:</h3>
    <div v-for="capstone in student.capstones">
      <h4>{{ capstone.name }}</h4>
      <h4>{{ capstone.description }}</h4>
      <router-link>
        <h4>{{  capstone.url }}</h4>
      </router-link>
      <img v-bind:src="capstone.screenshot_url">
    </div>
    <router-link v-bind:to="`/${student.id}/edit`">
      <button>edit</button>
    </router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      student: {},
      experience: [],
      education: [],
      skills: [],
      capstones: [],
    };
  },

  created: function () {
    axios.get("/api/students/" + localStorage.getItem("studentId")).then((response) => {
      this.student = response.data;
      this.experience = response.data.experiences;
      this.education = response.data.educations;
      this.skill = response.data.skills;
      this.capstone = response.data.capstones;
      console.log("show student info", this.student);
      console.log("show experience info", this.experience);
      console.log("show education info", this.education);
      console.log("show skill info", this.skill);
      console.log("show capstone info", this.capstone);
    });
  },

  methods: {},
};
</script>

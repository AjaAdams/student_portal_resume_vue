<template>
  <div class="about">
    <h1>This is an EDIT page</h1>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      resume: [],
      newStartDate: "",
      newEndDate: "",
      newJobTitle: "",
      newCompanyName: "",
      newDetails: "",
      newEdStartDate: "",
      newEdEndDate: "",
      newDegree: "",
      newUniversityName: "",
      newEdDetails: "",
      newSkillName: "",

    };
  },
  created: function() {
    // need to find a way to get current users info on next line
    axios.get("api/students").then(response => {
      this.resume = response.data;
      console.log("Here is the users resume", this.resume);
    });
  },
  methods: {
    updateResumeExperience: function(resume) {
      var params = {
        start_date: this.newStartDate,
        end_date: this.newEndDate,
        job_title: this.newJobTitle,
        company_name: this.newCompanyName,
        details: this.newDetails,
      };
      axios.patch("api/students/" + resume.id, params).then(response => {
        console.log("Experience Updated!", response.data);
      });
    },
    updateResumeEducation: function(resume) {
      var params = {
        start_date: this.newEdStartDate,
        end_date: this.newEdEndDate,
        degree: this.newDegree,
        university_name: this.newUniversityName,
        details: this.newEdDetails,
      };
      axios.patch("api/students/" + resume.id, params).then(response => {
        console.log("Education Updated!", response.data);
      });
    },
    updateResumeSkills: function(resume) {
      var params = {
        skill_name: this.newSkillName,
      };
      axios.patch("api/students/" + resume.id, params).then(response => {
        console.log("Skills Updated!", response.data);
      });
    },
  },
};
</script>
<template>
  <div class="about">
    <h1>This is an EDIT page</h1>
    <button>Update Personal Info</button>
    <button>Update Experience</button>
    <button>Update Education</button>
    <button>Update Skills</button>
    <button>Update Capstone</button>
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
      newCapName: "",
      newDescription: "",
      newUrl: "", 
      newScreenShotUrl: "",
      newFirstName: "",
      newLastName: "",
      newShortBio: "",
      newLinkedinUrl: "",
      newTwitterHandle: "",
      newPersonalWebsite: "",
      newOnlineResumeUrl: "",
      newGithubUrl: "",
      newPhotoUrl: "",

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
    updateResumeCapstone: function(resume) {
      var params = {
        name: this.newCapName,
        description: this.newDescription,
        url: this.newUrl,
        screenshot_url: this.newScreenShotUrl,
      };
      axios.patch("api/students/" + resume.id, params).then(response => {
        console.log("Capstone Updated!", response.data);
      });
    },
    updateResumeInformation: function(resume) {
      var params = {
        first_name: this.newFirstName,
        last_name: this.newLastName,
        short_bio: this.newShortBio,
        linkedin_url: this.newLinkedinUrl,
        twitter_handle: this.newTwitterHandle,
        personal_website_url: this.newPersonalWebsite,
        online_resume_url: this.newOnlineResumeUrl,
        github_url: this.newGithubUrl,
        photo_url: this.newPhotoUrl,
      };
      axios.patch("api/students/" + resume.id, params).then(response => {
        console.log("Information Updated!", response.data);
      });
    },
  },
};
</script>
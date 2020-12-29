<template>
  <div class="about">
    <h1>This is an EDIT page</h1>
    <p>First Name:
    <input type="text" v-model="newFirstName"></p>
    <p>Last Name:
    <input type="text" v-model="newLastName"></p>
    <p>Short Bio:
    <input type="text" v-model="newShortBio"></p>
    <p>LinkedIn URL:
    <input type="text" v-model="newLinkedinUrl"></p>
    <p>Personal Website URL:
    <input type="text" v-model="newPersonalWebsite"></p>
    <p>Online Resume URL:
    <input type="text" v-model="newOnlineResumeUrl"></p>
    <p>GitHub URL:
    <input type="text" v-model="newGithubUrl"></p>
    <p>Photo URL:
    <input type="text" v-model="newPhotoUrl"></p>
    <button v-on:click="updateResumeInformation(student)">Update Personal Info</button>
    <p>Start Date:
    <input type="text" v-model="newStartDate"></p>
    <p>End Date:
    <input type="text" v-model="newEndDate"></p>
    <p>Job Title:
    <input type="text" v-model="newJobTitle"></p>
    <p>CompanyName:
    <input type="text" v-model="newCompanyName"></p>
    <p>Details:
    <input type="text" v-model="newDetails"></p>
    <button v-on:click="updateResumeExperience(student)">Update Experience</button>
    <p>Start Date:
    <input type="text" v-model="newEdStartDate"></p>
    <p>End Date:
    <input type="text" v-model="newEdEndDate"></p>
    <p>Details:
    <input type="text" v-model="newEdDetails"></p>
    <p>Degree:
    <input type="text" v-model="newEdDegree"></p>
    <p>University Name:
    <input type="text" v-model="newEdUniversityName"></p>
    <button v-on:click="updateResumeEducation(student)">Update Education</button>
    <p>Skill Name:
    <input type="text" v-model="newSkillName"></p>
    <button v-on:click="updateResumeSkills(student)">Update Skills</button>
    <p>Capstone Name:
    <input type="text" v-model="newCapName"></p>
    <p>Capstone Description:
    <input type="text" v-model="newDescription"></p>
    <p>Capstone URL:
    <input type="text" v-model="newUrl"></p>
    <p>Capstone Screen Shot URL:
    <input type="text" v-model="newScreenShotUrl"></p>
    <button v-on:click="updateResumeCapstone(student)">Update Capstone</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      student: {},
      newStartDate: "",
      newEndDate: "",
      newJobTitle: "",
      newCompanyName: "",
      newDetails: "",
      newEdStartDate: "",
      newEdEndDate: "",
      newEdDegree: "",
      newEdUniversityName: "",
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
    axios.get("api/students").then(response => {
      this.student = response.data;
      console.log("Here is the users stuff", this.student);
    });
  },
  methods: {
    updateResumeExperience: function(student) {
      var params = {
        start_date: this.newStartDate,
        end_date: this.newEndDate,
        job_title: this.newJobTitle,
        company_name: this.newCompanyName,
        details: this.newDetails,
      };
      axios.patch("api/students/" + student.id, params).then(response => {
        console.log("Experience Updated!", response.data);
      });
    },
    updateResumeEducation: function(student) {
      var params = {
        start_date: this.newEdStartDate,
        end_date: this.newEdEndDate,
        degree: this.newEdDegree,
        university_name: this.newEdUniversityName,
        details: this.newEdDetails,
      };
      axios.patch("api/students/" + student.id, params).then(response => {
        console.log("Education Updated!", response.data);
      });
    },
    updateResumeSkills: function(student) {
      var params = {
        skill_name: this.newSkillName,
      };
      axios.patch("api/students/" + student.id, params).then(response => {
        console.log("Skills Updated!", response.data);
      });
    },
    updateResumeCapstone: function(student) {
      var params = {
        name: this.newCapName,
        description: this.newDescription,
        url: this.newUrl,
        screenshot_url: this.newScreenShotUrl,
      };
      axios.patch("api/students/" + student.id, params).then(response => {
        console.log("Capstone Updated!", response.data);
      });
    },
    updateResumeInformation: function(student) {
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
      axios.patch("api/students/" + student.id, params).then(response => {
        console.log("Information Updated!", response.data);
      });
    },
  },
};
</script>
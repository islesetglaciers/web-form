<template>
  <form @submit.prevent="handleSubmit">
      <label>Email :</label>
      <input type="email" required v-model="email">

      <label>Password :</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError" class="error">
          {{ passwordError }}
      </div>

      <label>Role :</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Web Designer</option>
      </select>

      <label>Skills :</label>
      <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
      <div v-for="skill in skills" :key="skill" class="pill">
          <span @click="removeSkill(skill)">{{ skill }}</span>
      </div>

      <!-- Checkbox w/ Booleans -->
      <div class="terms">
          <input type="checkbox" v-model="terms" required>
          <label>Accept terms and conditions</label>
      </div>

      <div class="submit">
          <button>Create an account</button>
      </div>

    <!-- Checkboxes w/ Arrays 
      <div>
          <input type="checkbox" value="Name" v-model="names" >
          <label>Name</label>
      </div>
      <div>
          <input type="checkbox" value="NameAgain" v-model="names" >
          <label>NameAgain</label>
      </div>
      <div>
          <input type="checkbox" value="YetAnotherName" v-model="names" >
          <label>YetAnotherName</label>
      </div>
    -->
  </form>
  <p>Email : {{ email }}</p>
  <p>Password : {{  password }}</p>
  <p>Role : {{  role }}</p>
  <p>Terms : {{  terms }}</p>
  <!-- <p>Names : {{  names }}</p> -->
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: false,
            names: [],
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill(e) {
            // console.log(e)
            if (e.key === ',' && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                    // console.log(this.skills)
                }
                this.tempSkill = '' 
            }
        },
        removeSkill(skill) {
            // My Solution
            // const index = this.skills.indexOf(skill)
            // if (index > -1) {
            //     this.skills.splice(index, 1)
            // }
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            // console.log('Form Submitted!')
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 characters long'
            if (!this.passwordError) {
                console.log('Email : ' + this.email)
                console.log('Password : ' + this.password)
                console.log('Role : ' + this.role)
                console.log('Skills : ' + this.skills)
                console.log('Terms : ' + this.terms)
            }
        }
    }
}
</script>

<style>
    form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    outline: none;
  }
  input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
  }
  .pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    color: #777;
    cursor: pointer;
  }
  button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
  }
  .submit {
    text-align: center;
  }
  .error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
  }
</style>
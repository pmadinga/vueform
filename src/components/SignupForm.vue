<template>
  <form @submit.prevent="handleSubmit">
    <label>Email</label>
    <input type="email" required v-model="email"/>

    <label>Password</label>
    <input type="password" required v-model="password"/>
    <div v-if="passwordErr" class="err">{{ passwordErr }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option disabled value="">Please select your role</option>
      <option value="developer">Web Developer</option>
      <option value="desinger">Web Designer</option>
    </select>

    <div class="terms">
      <input type="checkbox" required v-model="terms"/>
      <label>Accept terms and conditions</label>
    </div>

    <label for="">Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" pattern="[a-zA-Z0-9 ]+">
    <div v-for="(skill, index) in skills" :key="skill" class="pill">
      <span @click="removeSkill(skill)">{{ `${skill} - ${index}`}}</span>
    </div>

    <div class="submit">
      <button>Create Account</button>
    </div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>terms {{ terms }}</p>
</template>


<script>
  export default{
    data(){
      return{
        email: '',
        password: '',
        role: '',
        terms: false,
        tempSkill: '',
        skills: [],
        passwordErr: ''
      }
    },
    methods: {
      addSkill(evt){
   
        if(evt.key === ',' && this.tempSkill){
          if(! this.skills.includes(this.tempSkill)){
            this.skills.push(this.tempSkill)
          }
          this.tempSkill = ''
        }
      },
      removeSkill(skill){
        console.log(skill);
        this.skills.splice(skill, 1)
      },
      handleSubmit(){
        this.passwordErr = this.passwordErr.length > 5 ? 
          '' : 'Password length must be atleast 6 chars long'
        if(!this.passwordErr){
          console.log('email: ', this.email);
          console.log('password: ', this.password);
          console.log('role: ', this.role);
          console.log('skills: ', this.skills);
          console.log('terms: ', this.terms);
        }
      }
    }
  }
</script>
<style>
  form{
    max-width: 420px;
    margin: 30px auto;
    background: #fff;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label{
    display: inline-block;
    padding: 10px 6px;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: 500;
    font-size: 0.6rem;
    color: #aaa;
  }
  input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  input:focus{
    outline: none;
    box-shadow: none;
  }

  input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: none 10px 0 0;
    position: relative;
    top: 2px;
  }
  .pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }
  button{
    background-color: #0b6dff;
    border: none;
    padding: 10px 20px;
    margin-top: 20px;
    color: #fff;
    border-radius: 20px;
  }
  .submit{
    text-align: center;
  }
  .err{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8rem;
    font-weight: bold;
  }
</style>
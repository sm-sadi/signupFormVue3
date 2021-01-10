<template>
  <form @submit.prevent="handelSubmit">
      <label > Email:</label>
      <input type="email" required v-model="email">

      <label > Password:</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError" class="error">{{passwordError}}</div>
      

<!-- select from drop down list  -->
      <label for="">role :</label>
    <select name="" id="" v-model="role">
             <option value="Web-Developer">   Web developer </option>
             <option value="Designer">   Designer </option>
            <option  value="Manager">    Manager</option>
    </select>
<!-- check box to get the value as a boolean   -->

<!-- check box to get an array from the value   -->
<!-- <div class="Technology">
    <input type="checkbox" value="Node" v-model="Technology">
    <label>Node JS </label>
    <input type="checkbox" value="Express"  v-model="Technology">
    <label>Express JS </label>
    <input type="checkbox" value="Database"  v-model="Technology">
    <label>Database </label>
</div> -->


<!-- input with keyboard events  -->
<label >skills    <span class="hints" :class="{showH : showHi}">(press "alt + coma" to add)</span></label>
<input type="text" v-model="tempskills" @keyup.alt="addtoskill"  @mouseover="showhints">
<div v-for="skill in skills"  :key='skill' class="Skill">
  <span @click="deleteElement">{{skill}}</span>
  
    
</div>

<div class="terms" >
    <input type="checkbox" required v-model="terms">
    <label >Accept the Terms and conditions</label>
</div>

<div class="submit">
  <button>Create an Account</button>
</div>
  </form>

  <div class="data">
      <p> Data from the input flied : </p>
      <p> 
        Email : <span class="userData">{{email}}</span>  
        Password : <span class="userData">{{password}}</span> <br>
        Role :  <span class="userData">{{role}}</span>
        Temrs Accepted  : <span class="userData">{{terms}}</span><br>
        <!-- Knowledge of Technology :<span class="userData">{{Technology}}</span> -->
        skills  : <span class="userData">{{skills}}</span>
        </p>
  </div>
</template>

<script>
export default {
 data(){
     return{
         email : '',
         password :'',
         role : '',
         terms: false,
        //  Technology : []
        tempskills :[],
        skills: [],
        showHi: false,
        passwordError: ''
         
     }
 },
 methods : {
     addtoskill(e){
         if(e.key === "," && this.tempskills){
            if(!this.skills.includes(this.tempskills)){
              this.skills.push(this.tempskills)
            }

             this.tempskills =''

         }
     },
     showhints(){
       this.showHi = !this.showHi
     },
     deleteElement(e){
      //  console.log(e.currentTarget.innerHTML);
      //  this.skills.splice(e.currentTarget)
      this.skills = this.skills.filter(function(itm){
          return itm !== e.currentTarget.innerHTML
      })
     },
     handelSubmit(){
      //validate password
      // if(this.password.length <7 ){
      //   console.log("lenght is short");
      this.passwordError = this.password.length >7 ?
       '' : "password must be 7 chars long "
      }
     
     }
     
 }

</script>

<style>
form {
    max-width: 25rem;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    color: rgb(54, 52, 52);
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
  }
  input[type="checkbox"]{
      display: inline-block;
      width: 1rem;
      margin: 0 10px 0 0 ;
      position: relative;
      top: 2px;
  }
  .data{
    color: rgb(14, 14, 26);
    max-width: 25rem;
    margin: 10px auto;
    background: white;
    text-align: left;
    padding: 10px;
    border-radius: 10px;
  }
  .userData{
      color: darkblue;
  }
.Skill{
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
.hints{
  margin-left: 174px;
  color: rgb(80, 177, 80);
  visibility: hidden;
}
.showH{
  visibility: visible;
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
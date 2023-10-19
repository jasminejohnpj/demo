<template>
  <div class="header">
    <!-- <div class="img">
      <img
        :src="require(`~/components/adad.png`)"
        style="width: 40vw; height: 100vh"
      />
    </div> -->
    <div class="form">
      <h3>Sathyam vada Dharmam chara</h3>
      <div class="input-grp">
        <input type="text" v-model="firstName" placeholder="First Name" />
        <input type="text" v-model="lastName" placeholder="Last name" />
      </div>

      <div class="input-grp1">
        <input type="email" v-model="email" placeholder="Email" />
        <input id = "dob" type="date" v-model="dob" value="D O B" style="width: 100px" />
        <div class="radio">
          <img
            class="icon"
            :src="require(`~/components/gender.png`)"
            style="height: 40px"
          /><br />
          <div class="radio-grp">
          <input id = "radiobtn" type="radio" v-model="gender" name="gender" value="male" />
          <input id = "radiobtn" type="radio" v-model="gender" name="gender" value="female" />
          
          </div>
        </div>
      </div>
      <div class="input-grp3" style = "position: relative;left:0.7vw;">
        <select class="dropdowncountry" v-model="country" placeholder="country">
          <option value="" disabled selected>country</option>
          <option value="option1">Option 1</option>
          <option value="option2">Option 2</option>
          <option value="option3">Option 3</option>
        </select>
        <div class="phone" >
          <input
            type="text"
            placeholder="flag"
            class = "flag"
            style = "width:55px;padding-left:7px"
            
          />
          <input
            type="phone"
            v-model="phone"
            placeholder="Ph no"
            style = "width:70%; "    />
        </div>
      </div>
      <div class="input-grp2">
        <div class="head">
          <label class="hearabout">Where did you hear about thasmai ?</label>

          <ul class="radio-container">
            <li><label for="ReferSocial Media">Social Media</label></li>
            <li><label for="referReference">Reference</label></li>
            <li><label for="ReferNews">News</label></li>
          </ul>
          <ul class="list">
            <li><input name = "radio" type="radio" v-model="referenceoptn" value="Social Media"/></li>
            <li><input name = "radio" type="radio" v-model="referenceoptn" value="Reference" /></li>
            <li><input name = "radio" type="radio" v-model="referenceoptn" value="News" /></li>
          </ul>
        </div>
        
        <select class="dropdownlang" v-model="language" placeholder="Languages">
          <option value="" disabled selected>Languages</option>
          <option value="option1">English</option>
          <option value="option2">Malayalam</option>
          <option value="option3">Hindi</option>
        </select>
      </div>
      <div class="message">
        <textarea v-model="message" placeholder="Specialremarks"></textarea>
      </div>
      <button type="button" @click="submitForm">Submit</button>
    </div>
    <client-only placeholder="loading...">
     <script>
      let dob = document.getElementById("dob").value = ""
      console.log('qwert',dob)
     </script>
    </client-only>
    </div>

</template>

<script>
export default {
  data(){
    return{
      firstName:'',
      lastName:'',
      email:'',
      dob:'',
      gender:'',
      country:'',
      phone:'',
      referenceoptn:'',
      language:'',
      message:'',
    }
  },
  methods:{
   async submitForm(){
      const formData = {
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
        dob: this.dob,
        gender: this.gender,
        country: this.country,
        phone: this.phone,
        referenceOption: this.referenceOption,
        language: this.language,
        specialRemarks: this.message,
      };
      try {
        const response = await this.$axios.post(
          "http://localhost:3000/api/reistrations/registerUser",
          formData
        ); // Replace '/api/submitForm' with your API endpoint
        console.log(response.data);
        this.$router.push("/success");
      } catch (error) {
        // Handle any errors that occur during form submission
        console.error("Error submitting the form:", error);
      }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  max-width: 100vw;
}
.header {
  width: 100vw;
  height: 100vh;
  display: flex;
}
.header .img {
  width: 40%;
  height: 100vh;
}
.header .form {
  width: 60%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}
.header .form h3 {
  display: flex;
  position: absolute;
  justify-content: center;
  top: 20px;
}
.header .form .input-grp {
  width: 65%;
  display: flex;
  position: relative;
  justify-content: space-around;
  top: 40px;
}
.header .form .input-grp input {
  width: 40%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left:20px;
  box-sizing: border-box;
}
.header .form .input-grp1 {
  height:3vh;
  width: 65%;
 
  display: flex;
  position: relative;
  justify-content: space-around;
}

.header .form .input-grp1 input {
  width: 40%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left:20px;
  box-sizing: border-box;
}

.header .form .input-grp1 .radio.icon {
  width: 40px;
  height: 10px;
  display: flex;
  /* flex-direction: row; */
  justify-content: flex-start;
}

.header .form .input-grp1 .radio{
  position: relative;
  top:-20px;
}

.header .form .input-grp1 .radio img {
  width: 61px;
  height: 59px !important;
}
.header .form .input-grp1 .radio-grp{
display: flex;
justify-content: space-around;
position: relative;
top:-10px;
}
.header .form .input-grp1 .radio #radiobtn {
  width:18px;
  height:18px;
 
 
}
.header .form .input-grp3 {
  width: 65%;
  display: flex;
  position: relative;
  justify-content: space-around;
}
.header .form .input-grp3 .dropdowncountry {
  width: 40%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left:20px;
  box-sizing: border-box;
}
.header .form .input-grp3 .phone input{
  width: 40%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left:20px;
  box-sizing: border-box;
}
.header .form .input-grp2 {
  width: 65%;
  display: flex;
  position: relative;
  justify-content: space-around;
}

/* .header .form .input-grp2 .head {
  width: 80%;
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
} */

.header .form .input-grp2 .list {
display: flex;
width: 20vw;
list-style: none;
justify-content: space-around;
align-items: flex-start;
}
.header .form .input-grp2 .radio-container {
display: flex;
width: 20vw;
list-style: none;
justify-content: space-around;
align-items: flex-start;
}

.header .form .message textarea{
  width: 37vw;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left:20px;
  box-sizing: border-box;
  display: flex;
  align-items: center;
}
.header .form .input-grp2 .head{
  width: 50%;
}
.header .form .input-grp2 .head label{
  color:rgb(47, 47, 47);  
  
}



.header .form .input-grp2 .a select{
  width: 40%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left:20px;
  box-sizing: border-box;
}

.header .form button {
  width: 60%;
  height:40px;
  color:white;
  font-weight:400;
  border:none;
  
  
  border-radius:4px;
  background-color:rgb(182,157,106);
}
.header .form .input-grp2 .dropdownlang{
  width: 40%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left:20px;
  box-sizing: border-box;
}
</style>

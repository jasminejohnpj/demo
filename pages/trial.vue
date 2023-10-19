<template>
  <div class="header">
    <div class="homebtn">
    <button @click="toggleLoginForm">Sign Up</button>
    <select class="homelang" v-model="language" placeholder="Languages">
            <option value="" disabled selected>Languages</option>
            <option value="option1">English</option>
            <option value="option2">Malayalam</option>
            <option value="option3">Hindi</option>
          </select>
        </div>
    <div :class="{ 'login-container': true, 'show-login': isLoginVisible }">
      <div class="login-form">
        <h3>Sathyam vada Dharmam chara</h3>
        <div class="input-grp">
          <input type="text" v-model="firstName" placeholder="First Name" />
          <input type="text" v-model="lastName" placeholder="Last name" />
        </div>

        <div class="input-grp1">
          <input type="email" v-model="email" placeholder="Email" />
          <input id="dob" type="date" v-model="dob" value="D O B" style="width: 100px"/>
          <div class="radio">
            <img class="icon" :src="require(`~/components/gender.png`)" style="height: 40px"/>
            <div class="radio-grp">
              <input id="radiobtn" type="radio" v-model="gender" name="gender" value="female"/>
              <input id="radiobtn" type="radio" v-model="gender" name="gender" value="male"/>
            </div>
          </div>
        </div>
        <div class="input-grp3" style="position: relative; left: 0.7vw">
          <select class="dropdowncountry" v-model="selectedCountry" @click="getCountryInfo" >
  <option value="" disabled selected>country</option>
  <option v-for="country in selectedCountry" :key="country.id">
    {{ country.id.name }}
  </option>
</select>
          <div class="phone">
            <input type="text" placeholder="flag" class="flag" style="width: 55px; position: relative; left:2.5vw; margin-right: 33px; padding-left: 7px"/>
            <input type="phone" v-model="phone" placeholder="Ph no" style="width: 60%"/>
          </div>
        </div>
        <div class="input-grp2">
          <div class="head">
           <span><img 
              class="lens"
              :src="require(`~/components/lens.jpeg`)"
              style="height: 20px;position: relative !important; left: 0vw;top: 1vw !important;"></span>
            <ul class="radio-container">
              <li><label for="ReferSocial Media">Social Media</label>
                <input name="radio" type="radio" v-model="referenceoptn" value="Social Media"/></li>
              <li><label for="referReference">Reference</label>
                <input name="radio" type="radio" v-model="referenceoptn" value="Reference"/></li>
              <li><label for="ReferNews">News</label><input name="radio" type="radio" v-model="referenceoptn" value="Reference"/></li>
            </ul>
          </div>
          <select class="dropdownlang" v-model="language" placeholder="Languages">
            <option value="" disabled >selected Languages</option>
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
          let dob = (document.getElementById("dob").value = "");
          console.log("qwert", dob);
        </script>
      </client-only>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      isLoginVisible: false,
      firstName: '',
      lastName: '',
      email: '',
      dob: '',
      gender: '',
      selectedCountry: [],
      flag:[],
      digitalCode:[],
      phone: 'digitalCode' +'',
      referenceoptn: '',
      language: '',
      message: '',
    };
  },
  methods: {
    toggleLoginForm() {
      this.isLoginVisible = !this.isLoginVisible;
    },
      




    async getCountryInfo() {
     
      try {
    const response = await axios.get('http://192.168.1.73:3000/api/reistrations/countrieslist');
    const countryData = response.data;
    this.selectedCountry = countryData;
    const countryNames = countryData.map(country => country.name)
    this.selectedCountry = countryNames;
    const flags=countryData.map(country=> country.flag)
    this.flag=flags;
    const code= countryData.map(country=> country.phonecode)
    this.digitalCode=code;
    console.log(countryNames)
    console.log(flags);
    console.log(code);
    
    this.updateCountryInfo();
  } catch (error) {
    console.error('Error fetching country information', error);
    throw error;
  }
},
updateCountryInfo() {
    // Assuming you have the selected country stored in this.selectedCountry
    const selectedCountry = this.selectedCountry;
    // Retrieve the corresponding flag and digital code
    const flag = selectedCountry.flags; // Assuming this is the correct property for the flag
    const digitalCode = selectedCountry.phonecode; // Assuming this is the correct property for the digital code

    // Update the data properties accordingly
    this.flag = flag;
    this.digitalCode = digitalCode;
  },
    
    async submitForm() {
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
          "http://192.168.1.38:3000/api/reistrations/registerUser",
          formData
        ); // Replace '/api/submitForm' with your API endpoint
        console.log(response.data);
        this.$router.push("/success");
      } catch (error) {
        // Handle any errors that occur during form submission
        console.error("Error submitting the form:", error);
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
}
.header {
  margin: 0;
  padding: 0;
  height: 100vh;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  flex-direction: column;
  background-image: url("../components/step.jpg");
  background-size: cover;
}
.header .homebtn{
  width:200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin:0 0 0 10px;
  
}
.header .homebtn button {
  width: 60%;
  height: 30px;
  font-weight: 400;
  border: none;
  border-radius: 4px;
  background-color: rgb(182, 157, 106);
  margin-top: 100px;
}
.homelang{
  width: 60%;
  height: 30px;
  font-weight: 400;
  border: none;
  border-radius: 4px;
  background-color: rgb(182, 157, 106);
}
.login-container {
  position: absolute;
  right: 0;
  top: 0;
  height: 100%;
  width: 70%;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(148, 142, 142, 0.8);
  /* background-image: url('1.png'); */
  color: #fff;
  transition: transform 0.5s;
  transform: translateX(100%); /* Start off-screen to the right */
}
.login-form {
  display: flex;
  /* text-align: center; */
  width: 70%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.show-login {
  transform: translateX(0); /* Move to the visible area (left) */
}
.header .login-container .login-form h3 {
  display: flex;
  position: absolute;
  justify-content: center;
  top: 20px;
}
.header .login-container .login-form .input-grp {
  width: 70%;
  display: flex;
  position: relative;
  justify-content: space-around;
  top: 40px;
  margin-right: 3vh;
}
.header .login-container .login-form .input-grp input {
  width: 45%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left: 20px;
  box-sizing: border-box;
}
.header .login-container .login-form .input-grp1 {
  height: 3vh;
  width: 70%;
  display: flex;
  position: relative;
  justify-content: space-around;
}
.header .login-container .login-form .input-grp1 input {
  width: 45%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left: 20px;
  box-sizing: border-box;
  position: relative;
  margin-left: -2vh;
}
.header .login-container .login-form .input-grp1 .radio.icon {
  width: 40px;
  height: 10px;
  display: flex;
  /* flex-direction: row; */
  justify-content: flex-start;
}
.header .login-container .login-form .input-grp1 .radio {
  position: relative;
  top: -20px;
}
.header .login-container .login-form .input-grp1 .radio img {

    width: 58px;
  height: 59px !important;
}
.header .login-container .login-form .input-grp1 .radio-grp {
  display: flex;
  justify-content: space-around;
  position: relative;
  top: -10px;
}
.header .login-container .login-form .input-grp1 .radio #radiobtn {
  width: 18px;
  height: 18px;
}
.header .login-container .login-form .input-grp3 {
  width: 70%;
  display: flex;
  position: relative;
  justify-content: space-around;
}
.header .login-container .login-form .input-grp3 .dropdowncountry {
  width: 48%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left: 20px;
  box-sizing: border-box;
}
.header .login-container .login-form .input-grp3 .phone{
  width: 300px;
}
.header .login-container .login-form .input-grp3 .phone input {
  width: 40%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left: 20px;
  box-sizing: border-box;
}
.header .login-container .login-form .input-grp2 {
  width: 70%;
  display: flex;
  position: relative;
  justify-content: space-around;
}
.header .login-container .login-form .input-grp2 .radio-container {
  display: flex;
  width: 17vw;
  height: 40%;
  list-style: none;
  justify-content: space-around;
  align-items: flex-start;
  margin-right: 20px;
  position: relative;
  top:-1.5vh;
  
  
  left:-1vw;
}
.header .login-container .login-form .message textarea {
  width: 35vw;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left: 20px;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  position: relative;
  top: -12vh;
}
.header .login-container .login-form .input-grp2 .head {
  width: 55%;
  height: 60%;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  margin-left: 5px;
 position: relative;
 top: -6vh;
  box-sizing: border-box;
 
  
  
  background-color:white;
  color:black;
}
.header .login-container .login-form .input-grp2 .head .radio-container .lens{
  width: 20px;
  height: 20px;
  margin-right:2px;
  display: flex;
  justify-content: flex-start;

}
.header .login-container .login-form .input-grp2 .a select {
  width: 40%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left: 20px;
  box-sizing: border-box;
}
.header .login-container .login-form button {
  width: 65%;
  height: 40px;
  color: white;
  font-weight: 400;
  border: none;
  border-radius: 4px;
  background-color: rgb(182, 157, 106);
  position: relative;
  top:-17vh;
}
.header .login-container .login-form .input-grp2 .dropdownlang {
  width: 36%;
  height: 40px;
  border: 0.3px solid rgba(206, 206, 206, 0.6);
  border-radius: 4px;
  margin-bottom: 20px;
  padding-left: 20px;
  box-sizing: border-box;
  position: relative;
  top: -20vh;
}
</style>

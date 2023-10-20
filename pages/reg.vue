<template>
    
    <div class="reg-hero">

       <div class="hero-right">
           <div class="hero-right-content">
       <h3 class = 'hero-right-heading'>Sathyam vada || dharmam chara <button class = "play-btn"><img :src="require(`~/components/playbutton.png`)"></button></h3>
           <div class="hero-right-input-grp">
               
               
               <div class="input-grp" style="
               position: relative;
               top: -1vw;">
                   <input type="text" class="label" placeholder="First name" v-model="firstname">
                   <input type="text" class="label" placeholder="Last name" v-model="lastname">

               </div>
               <div class="input-grp dob-grp ">
                   <input type="text" class="label" placeholder="Email" v-model="email" style="
                   width: 16vw;
                   position: relative;
                   left: 0.4vw;">
                   <input type="text" class="label dob" placeholder="DOB" v-model="dob">
                   <div class="hero-right-radio-grp">
                   <img :src="require(`~/components/gender.png`)" class = "gender">
                       <div class="hero-right-radio-btn-grp">
                           <input type="radio" v-model="gender" value="female">
                           <input type="radio" v-model="gender" value="male">
                       </div>
               </div>
               </div>
               <div class="input-grp country-grp">
                   <select class="label" v-model="country" :items="countries" @click="getCountryInfo" style="
                   position: relative;
                   left: 0.5vw;
                   width:16.5vw;
               ">
           <option>Country</option>  
           <option v-for="country in countries" :key="country.id" :value="country.name">
    {{ country.name }}
  </option>  
           </select>

                  <div class = "country-dropdown"> 
                    <img  :src="getFlag(selectedCountry)" height = "35"/></div>
                   <input class = "phone" type="text"  placeholder="+91">

               </div>
               <div class="bottom-grp">
               <div class="input-grp">
                   <div class="ref-grp">
                       <img src = "" alt = "icon">
                       <div class="ref-sub-grp">
                           <h6>Social media</h6>
                           <input type = 'radio' v-model="reference" value="socialmedia">
                       </div>
                       <div class="ref-sub-grp">
                           <h6>Reference</h6>
                           <input type = 'radio' v-model="reference" value="Reference">
                       </div>
                       <div class="ref-sub-grp">
                           <h6>News</h6>
                           <input type = 'radio' v-model="reference" value="news">
                       </div>
                   </div>
                   <select class="label" style = "width:16.5vw" v-model="selectedlanguage">
                       <option>Languages</option>
                   </select>

               </div>
               <div class="input-grp">
                   <input type="text" class="remarks" placeholder="Special remarks" v-model="remarks">

               </div>
               <div class="submit">
                   <button>Submit</button>
               </div>
           </div>
           
           <div class="hero-right-ribbon">
               <div class="ribbon-grp">
                   <h5>39997</h5>
                   <h6>Total meditators</h6>
               </div>
               <div class="ribbon-grp">
                   <h5>39997</h5>
                   <h6>Total meditators</h6>
               </div>
               <div class="ribbon-grp">
                   <h5>39997</h5>
                   <h6>Total meditators</h6>
               </div>
               <div class="ribbon-grp">
                   <h5>39997</h5>
                   <h6>Total meditators</h6>
               </div>
           </div>
           </div>
       </div>

       </div>
   </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return{
            firstname:'',
            lastname:'',
            email:'',
            dob:'',
            gender:'',
            country:'',
            selectedCountry:[],
            countries:[],
            flag:[],
            digitalCode:[],
            reference:'',
            selectedlanguage:'',
            remarks:'',
        }
    },
    mounted(){
      this.getCountryInfo();
  },
  computed: {
  formattedPhoneNumber: {
    get() {
      return this.phone;
    },
    set(value) {
      const code = this.getPhoneCode(this.selectedCountry);
      const phone = value.replace('' + code, '').trim(); // removing the code from the input value
      this.phone = phone;
    },
  },
},
 async getCountryInfo() {
     
      try {
    const response = await axios.get('http://192.168.1.73:3000/api/reistrations/countrieslist');
    const countryData = response.data;
    this.countries = countryData;
    this.countryNames = countryData.map((country) => country.name);
    this.flags = countryData.map((country) => country.flag);
    this.digitalCodes = countryData.map(country=> country.phonecode)
    // console.log(this.countryNames);
    // console.log(this.flags);
    // console.log(this.digitalCodes);
 
  } catch (error) {
    console.error('Error fetching country information', error);
    throw error;
  }
},

getFlag(selectedCountry) {
    const index = this.countryNames ? this.countryNames.indexOf(selectedCountry) : -1;
    if (index !== -1 && this.flags && this.flags.length > index) {
      return this.flags[index];
    }
    return '';
  },
  getPhoneCode(selectedCountry) {
    const index = this.countryNames ? this.countryNames.indexOf(selectedCountry) : -1;
    if (index !== -1 && this.digitalCodes && this.digitalCodes.length > index) {
      return this.digitalCodes[index];
    }
    return '';
  },
  methods:{
     toggleLoginForm() {
      this.isLoginVisible = !this.isLoginVisible;
    },
    async getCountryInfo() {
     
     try {
   const response = await axios.get('http://192.168.1.73:3000/api/reistrations/countrieslist');
   const countryData = response.data;
   this.countries = countryData;
   this.countryNames = countryData.map((country) => country.name);
   this.flags = countryData.map((country) => country.flag);
   this.digitalCodes = countryData.map(country=> country.phonecode)
   // console.log(this.countryNames);
   // console.log(this.flags);
   // console.log(this.digitalCodes);

 } catch (error) {
   console.error('Error fetching country information', error);
   throw error;
 }
},

getFlag(selectedCountry) {
   const index = this.countryNames ? this.countryNames.indexOf(selectedCountry) : -1;
   if (index !== -1 && this.flags && this.flags.length > index) {
     return this.flags[index];
   }
   return '';
 },
 getPhoneCode(selectedCountry) {
   const index = this.countryNames ? this.countryNames.indexOf(selectedCountry) : -1;
   if (index !== -1 && this.digitalCodes && this.digitalCodes.length > index) {
     return this.digitalCodes[index];
   }
   return '';
 },
  }
}
</script>

<style>
*{
    margin:0;
    font-family: 'Poppins', sans-serif;
    max-width:100vw;
}

.reg-hero{  
    width:100vw;
    height:100vh;
    display: flex;
}
.reg-hero .hero-right-heading{
    display:flex;
    justify-content:center;
    margin:5vh 0 5vh 0;
    font-size:17px;
}
.reg-hero .hero-right-content{

height:100vh;
position: relative;
top:7vh;

}
.hero-right-input-grp{
    width:40vw !important;
}
.hero-right-input-grp .input-grp .label{
    width: 16vw;
    height:6vh;
    border-radius:5px;
    border:none;
    border:0.5px solid rgba(0,0,0,0.3);
    box-shadow: 0px 7px 10px rgba(0,0,0,0.2 );
    outline:none;
  }
.hero-right-input-grp .input-grp{
    display: flex;

    justify-content: space-around;
}
.hero-right-input-grp .remarks{
    width: 92%;
    height:6vh;
    border:none;
    
    outline: none;
    border-radius:5px;
    border:0.5px solid rgba(0,0,0,0.3);
    box-shadow: 0px 7px 10px rgba(0,0,0,0.2)}
.hero-right-input-grp .submit button{
    width:94%;
    height:7vh;
    border:none;
    background-color: rgba(0,0,0,0.7);
    border:none;
    border:0.5px solid rgba(0,0,0,0.3);
    box-shadow: 0px 7px 10px rgba(0,0,0,0.7);
    color:white;
    border-radius:5px;
    
    position: relative;
    left:1.5vw;

}

.country-dropdown{
    position: relative;
    left: 1.5vw;
    width:4vw;
    height:6vh;
    border-radius:5px;
    border:none;
    border:0.5px solid rgba(0,0,0,0.3);
    display: flex;
    
    justify-content: center;
    align-items: center;
    border-radius:5px;
}
.country-grp{
    display: flex;
    position: relative;
    top:-5vw;
}
.count-grp .phone{
    width:11vw;
}
.gender{
    height:7vh;
}
.hero-right-content{
    
    display: flex;
    flex-direction:column;
    justify-content: space-around;
}
.hero-right-input-grp{
    width:100vh;
    height:100vh;
    display: flex;
    flex-direction:column;
    justify-content: space-around;
}

.ref-grp{
    width:17vw;
    display: flex;
    justify-content:space-around;
    align-items: center;
    
    border:0.5px solid rgba(0,0,0,0.3);
    border-radius:5px;
}
.ref-grp .ref-sub-grp{
    display:flex;
    flex-direction: column;
  
}
/* footer ribbon */
.dob-grp{
    display: flex;
    position: relative;
    top:-2vw;
}
.dob-grp .dob{
    width:12vw !important;
    position: relative;
    left:1.5vw;
}
.bottom-grp{
    
    height:12vw!important;
    display:flex;
    flex-direction: column;
   justify-content: space-between;
    position:relative;
    top:-6.5vw;
}
.hero-right-radio-btn-grp{





    display: flex;


    justify-content: space-around;
    position: relative;
    top:-1vw;
}
.hero-right-content .hero-right-ribbon{
    color:red;
    display: flex;
    justify-content: space-between;
    position: relative;
    
    

    top:-17vh;
}
.hero-right-content .hero-right-ribbon .ribbon-grp{
    display: flex;

    flex-direction:column;
    align-items:center;
    /* margin:5vh 0 0 0; */
}
</style>
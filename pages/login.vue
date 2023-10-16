<template>
  <div class="header">
    <div class="img">
      <img :src="require(`~/components/adad 2.png`)" style=" width: 500px; height: 600px;">
    </div>
    <div class="form">
      <h3>Sathyam vada Dharmam chara</h3>
    <div class="input-grp">
      <input type="text" placeholder="First name" />
      <input type="text" placeholder="Last name" />
    </div>

    <div class="input-grp1">
      <input type="email" placeholder="Email" />
      <input type="date" placeholder="D O B" style="width: 80px;" />
      <div class="radio">
      <img class="icon" :src="require(`~/components/gender.png`)" style="height: 50px;"/><br>
      <input type="radio" name="gender" value="male" />
      <input type="radio" name="gender" value="female" />
    </div>
</div>
    <div class="input-grp3">
      <select class="dropdowncountry" placeholder="country">
        <option value="" disabled selected>country</option>
        <option value="option1">Option 1</option>
        <option value="option2">Option 2</option>
        <option value="option3">Option 3</option>
      </select>
      <div class="phone">
      <input type="text" placeholder="flag" style="width: 40px; height:30px; border: .25px solid; border-radius:7px;">
      <input type="phone" placeholder="Ph no"  style="width: 150px; height:30px; border: .25px solid; border-radius:7px;">
    </div>
</div>
    <div class="input-grp2">
      <label>Where did you hear about thasmai ?</label>
    
      <div class="radio-container">
      <label for="ReferSocial Media">Social Media</label>
      <input type="radio" name="referenceoptn" value="Social Media" />
      <label for="referReference">Reference</label>
      <input type="radio" name="referenceoptn" value="Reference" />
      <label for="ReferNews">News</label>
      <input type="radio" name="referenceoptn" value="News" />
      </div>
      <select class="dropdownlang" placeholder="Languages">
        <option value="" disabled selected>Languages</option>
        <option value="option1">English</option>
        <option value="option2">Malayalam</option>
        <option value="option3">Hindi</option>
      </select>
    </div>
    <div class="message">
      <textarea
        name="message"
        placeholder="Special remarks"
      ></textarea>
    </div>
    <button type="button">Submit</button>
</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      phoneNumber: "",
    };
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
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
.header .form{
    width: 60%;
    height:100vh ;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
   
}
.header .form h3{
    display: flex;
    position: absolute;
    justify-content: center;
    top: 20px;
}
.header .form .input-grp{
    width: 65%;
    display: flex;
    position: relative;
    justify-content: space-around;
    top:50px; 
}
.header .form .input-grp1{
    width: 65%;
    display: flex;
    position: relative;
    justify-content: space-around;
    top:20px; 
}
.header .form .input-grp input{
    width: 40%;
    height: 30px;
    border: .25px solid;
   border-radius: 7px;
   margin-bottom: 20px;
}
.header .form .input-grp1 input{
    width: 40%;
    height: 30px;
    border: .25px solid;
   border-radius: 7px;
   margin-bottom: 20px;
}
.header .form .input-grp .icon{
    width: 40px;
    height: 30px;
    display: flex;
  flex-direction: row;
  justify-content: flex-start;
}
.header .form .input-grp1 .radio input[type="radio"] {
  width: 10px;
  height: 10px;
  position: relative;

  
} 

.header .form .input-grp p{
    position: relative;
    display: flex;
    justify-content: flex-start;
    
}
.header .form .input-grp3{
    width: 65%;
    display: flex;
    position: relative;
    justify-content: space-around;
  
}
.header .form .input-grp3 .dropdowncountry  {
    width: 40%;
    height: 30px;
    border: .25px solid;
   border-radius: 7px;
   margin-bottom: 20px;
}
.header .form .input-grp3 .phone{
    width: 200px;
    display: flex;
    justify-content: space-between;
}
.header .form .input-grp2{
    width: 65%;
    display: flex;
    position: relative;
    justify-content: space-around;
  
}
.header .form .input-grp2 .dropdownlang  {
    width: 40%;
    height: 30px;
    border: .25px solid;
   border-radius: 7px;
   margin-bottom: 20px;
}
.header .form .input-grp2 .radio-container {
  display: flex;

  flex-direction: row;
  align-items: center;
}

.radio-container label {
  margin-right: 10px;
}

.radio-container input[type="radio"] {
  width: 20px;
  height: 20px;
}
.header .form .message textarea{
    height: auto;
    min-height: 30px;
    width: 100%;
}
.header .form button{
    width: 60%;
}
</style>

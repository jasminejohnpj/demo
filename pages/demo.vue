<template>
    <div class="special-remarks">
        <p>Where did you hear about thasmai ?</p>
        <div class="demo">
  <label for="ReferSocialMedia">Social Media</label>
  <input type="radio" name="referenceoptn" value="Social Media" />
  <br>
  <label for="referReference">Reference</label>
  <input type="radio" name="referenceoptn" value="Reference" />
  <br>
  <label for="ReferNews">News</label>
  <input type="radio" name="referenceoptn" value="Reference" />
    </div>
</div>
    </template>

    <style>
    .special-remarks {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-top: 20px;
}



.special-remarks label {
  margin-top: 10px;
}
.special-remarks .demo{
    display: flex;
    position: relative;
}
.special-remarks .demo input[type="radio"] {
  width: 20px;
  height: 20px;
  display: flex;
  position: absolute;
  flex-direction: column;
  justify-content: flex-start;
}

    </style>
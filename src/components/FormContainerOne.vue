<template>
  <div class="bottom-layer ml-20">
    <div class="steps">
      <span class="bg-gradient-to-r from-blue-100 to-blue-100 p-3.5 py-2 rounded-xl">1</span> of <span id="total-steps">12</span>
    </div>
    <div class="move-icons">
      <i class="fa-solid fa-circle-chevron-left" id="left"></i>
      <i
        id="right"
        class="fa-solid fa-circle-chevron-left"
        @click="handleRightClick"
      ></i>
    </div>
  </div>
  <div class=" flex flex-col gap-5 rounded-3xl drop-shadow-md backdrop-blur box-border p-7 bg-gradient-to-r from-blue-100 to-blue-100 container white">
     
     <div class="flex gap-16">
      <label for="name" class=" font-semibold text-xl mt-2">Name</label>
      <div class="input-wrapper">
        <input type="text" v-model="name" @input="validateName" class=" nameInput h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" /><i
          id="correct"
          class="fa-solid fa-circle-check"
          v-if="CorrectName && name"
        ></i>
        <i
          id="cross"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectName && name"
        ></i>
      </div>
    </div>
    <div class="flex gap-14">
      <label class="font-semibold text-xl mt-2" for="theme" >Theme</label>
      <select name="theme" id="theme" v-model="theme" class="themeInput h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-2 pr-11 box-border align-middle">
        <option value="T1">
          Generic
        </option>
        <option value="T2">vegitation</option>
        <option value="T3">hydrology</option>
        <option value="T4">environment</option>
        
      </select>
    </div>
    <div class="flex gap-5">
      <label for="subtheme" class="font-semibold text-xl mt-2">Subtheme</label>
      <select name="subtheme" class=" subthemeInput h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-2  pr-8 pl-4 align-middle" v-model="subtheme">
        <option value="S1">Generic</option>
        <option value="S2">subtheme1</option>
        <option value="S3">subtheme2</option>
        <option value="S4">subtheme3</option>
      </select>
    </div>
     <div class="flex gap-5">
      <label for="productId_id" class="font-semibold text-xl mt-2">Product Id</label>
      <div class="input-wrapper">
        <input type="text" class="nameInput h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border " v-model="productId" @input="validateproductId" /><i
          id="correct"
          class="fa-solid fa-circle-check"
          v-if="CorrectproductId && productId"
        ></i>
        <i
          id="cross"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectproductId && productId"
        ></i>
      </div>
    </div>
    <div class="flex gap-6">
      <label for="sourcelocation" class="font-semibold text-xl mt-2">Source<br>Locations</label>
      <div class="input-wrapper">
        <input type="text" class=" w-full h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" v-model="sourcelocation" @input="validatesourcelocation" @keydown="handleCommaPress"/><i
          id="correct"
          class="fa-solid fa-circle-check"
          v-if="Correctsourcelocation && sourcelocation"
        ></i>
        <i
          id="cross"
          class="fa-solid fa-circle-xmark"
          v-if="!Correctsourcelocation && sourcelocation"
        ></i>
      </div>
    </div>
  </div>
  
 
</template>

<script>
import { ref, getCurrentInstance } from "vue";
import useValidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";
export default {
  /*
  // data() {
  //   return {
  //     v$: useValidate(),
  //     Correctsourcelocation: false,
  //     theme: "",
  //     subtheme: "",
  //     sourcelocation: "",
  //   };
  // },
  validations() {
    return {
      theme: { required },
      subtheme: { required },
      sourcelocation: { required },
    };
  },
  methods: {
    validatesourcelocation() {
      this.Correctsourcelocation = this.sourcelocation.startsWith("/");
    },
  */

  setup(props, { emit }) {
    const theme = ref("");
    const subtheme = ref("");
    const sourcelocation = ref("");
    const Correctsourcelocation = ref(false);
    const sourceLocationArray = ref([]);
    const CorrectproductId = ref(false);
    const productId = ref("");
    const v$ = useValidate();
    const name = ref("");
    const CorrectName = ref(true);
    function validatesourcelocation() {
      Correctsourcelocation.value = sourcelocation.value.startsWith("/");

    }


    const handleCommaPress = (event) => {
       if (event.key === ",") {
    const values = sourcelocation.value.split(",");
    sourceLocationArray.value = []; // Clear the array before adding new values
    values.forEach((value) => {
      const trimmedValue = value.trim();
      if (trimmedValue) { // Check if the trimmed value is not empty
        sourceLocationArray.value.push(trimmedValue);
      }
    });
    console.log(sourceLocationArray.value);
  }
        
    };

    const handleRightClick = () => {
      //logic for handling ID
      const id = theme.value + subtheme.value + productId.value; 
      console.log("this is id"+ id);

      const themeString = mapThemeToString(theme.value);
      const subthemeString = mapSubthemeToString(subtheme.value);



      // Emit an event to the parent component
      // This event is caught in the parent component to proceed to the next step
      console.log("emiting");
      console.log("src location:" + sourceLocationArray.value )

      const data = {
        subtheme: subthemeString,
        theme: themeString,
        sourcelocation: sourcelocation.value,
        name: name.value,
        productId : productId.value,
        id : id,
        sourcelocations: sourceLocationArray.value,
      };
      // Emit the 'update-data' event with the updated data
      emit("update-data", data);
      console.log(id);
    
      emit("validate-and-proceed", subtheme.value, theme.value, sourcelocation.value, productId.value, name.value);

      console.log(themeString);
    };

    const validateproductId = ()=>{
       CorrectproductId.value = productId.value.length < 50 && productId.value.length > 2;
    }

    const mapThemeToString = (themeValue) => {
      switch (themeValue) {
        case "T1":
          return "Generic";
        case "T2":
          return "Vegitation";
        case "T3":
          return "Hydrology";
        case "T4":
          return "Environment";
        default:
          return "";
      }
    };

    const mapSubthemeToString = (subthemeValue) => {
      switch (subthemeValue) {
        case "S1":
          return "Generic";
        case "S2":
          return "Subtheme1";
        case "S3":
          return "Subtheme2";
        case "S4":
          return "Subtheme3";
        default:
          return "";
      }
    };

    return {
      theme,
      subtheme,
      sourcelocation,
      CorrectName,
      Correctsourcelocation,
      validatesourcelocation,
      handleRightClick,
      CorrectproductId,
      productId,
      validateproductId,
      name,
      v$,
      handleCommaPress,
    };
  },
};
</script>

<style scoped>

.subthemeInput{
  width: 100%;

}
.white{
  width: 150%;
}

.nameInput{
  width: 100%;
}
.themeInput{
  width: 100%;
}
body {
  margin: 0;
  padding: 0;
  height: 100%;
}

.form-container-one {
  
}
.input-wrapper{
  position: relative;
}

#correct {
  color: green;
  position: absolute;
  z-index: 999;
  font-size: 18px;
  right: 2%;
  margin-top: 12px;
  
}

#cross {
  color: crimson;
  position: absolute;
  z-index: 999;
  font-size: 18px;
  right: 2%;
  margin-top: 12px;
}

#left {
  opacity: 0.8;
}

.bottom-layer {
  width: 100%;
  padding: 20px;
  text-align: center;
  font-size: 25px;
  padding-top: 30px;
  display: flex;
  gap: 15px;
  justify-content: center;
}

.themetext,
.subthemetext,
.productId-text {
  margin-top: 5px;
  font-weight: 600;
  font-size: 23px;
}

#current-step {
  background: linear-gradient(
    to bottom,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1
  ); /* Gradient fill */
  padding: 15px 20px 12px 20px;
  border: none;
  border-radius: 16px;
  box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.2);
}

#subtheme {
  width: 439px; /* Adjust as needed */
  height: 41px; /* Adjust as needed */
  border: none;
  border-radius: 50px; /* Half of the height */
  background: linear-gradient(
    to bottom,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1
  ); /* Gradient fill */
  color: #344747;
  font-size: 17px;
  text-indent: 10px;
  font-style: italic;
  box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.2);
  padding: 5px;
  font-weight: 300;
  position: relative;
    left: 80px;
}

.sourcelocation input {
  width: 439px; /* Adjust as needed */
  height: 41px; /* Adjust as needed */
  border: none;
  border-radius: 50px; /* Half of the height */
  background: linear-gradient(
    to bottom,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1
  ); /* Gradient fill */
  color: #344747;
  font-size: 17px;
  padding: 0;
  font-style: italic;
  box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.2);
  text-indent: 22px;
  font-weight: 300;
  box-sizing: border-box;
  margin-left: 4px;
}

.productId_id input{
width: 439px; /* Adjust as needed */
  height: 41px; /* Adjust as needed */
  border: none;
  border-radius: 50px; /* Half of the height */
  background: linear-gradient(
    to bottom,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1,
    #b2e2f1
  ); /* Gradient fill */
  color: #344747;
  font-size: 17px;
  padding: 0;
  font-style: italic;
  box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.2);
  text-indent: 22px;
  font-weight: 300;
  box-sizing: border-box;
  margin-left: 80px;
}

.name input{

}

.base-path-text {
  margin-top: 5px;
  font-weight: 600;
  font-size: 23px;
}

.name-text {
  margin-top: 5px;
  font-weight: 600;
  font-size: 23px;
}

.subtheme,
.sourcelocation,
.productId_id,
.name,
.theme {
  display: flex;
  gap: 10px;
}

.sourcelocation, .productId_id {
  box-sizing: border-box;
}

select {
  padding-right: 25px;
  box-sizing: border-box;
}

#right {
  transform: rotate(180deg);
  position: relative;
  left: 5px;
}

.theme {
  gap: 52px;
}

/* Base styles */

/* Styles for small phones (portrait and landscape) */
@media only screen and (max-width: 480px) {
  /* Your CSS rules for small phones */

  input{
    width: 0px;
    height: 0px;
  }

  .name{
    gap: 51px;
  }

  .name input,.productId_id input,.sourcelocation input{
    margin-top: 6px;
    margin-left:0;
    width: 150px;
    height: 23px;
  }

  #theme,#subtheme{
    margin-top: 6px;
    left: 0;
    width: 150px;
    height: 23px;
  }
  .theme{
    gap: 42px;
  }

  .name-text{
    font-size: 18px;
  }

  .themetext,.subthemetext,.base-path-text,.productId-text{
    font-size: 18px;
  }
  .sourcelocation{
    gap: 18px;
  }

  .form-container-one{
    padding: 35px 27px 37px 27px;
  }
  .bottom-layer{
    width: 90%;
    font-size: 25px;
  }
}

/* Styles for big phones (landscape) and small tablets */
@media only screen and (min-width: 481px) and (max-width: 767px) {
  /* Your CSS rules for big phones and small tablets */
}

/* Styles for big tablets and small laptops */
@media only screen and (min-width: 768px) and (max-width: 1023px) {
  /* Your CSS rules for big tablets and small laptops */
}

/* Styles for big laptops and desktops */
@media only screen and (min-width: 1024px) and (max-width: 1199px) {
  /* Your CSS rules for big laptops and desktops */
}

/* Styles for big desktops */
@media only screen and (min-width: 1200px) {
  /* Your CSS rules for big desktops */
}

</style>

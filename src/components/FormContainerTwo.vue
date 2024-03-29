<template>
  <div class="form-container-two">
    <div class="flex flex-col w-full gap-5 rounded-3xl drop-shadow-md backdrop-blur box-border p-7 bg-gradient-to-r from-blue-100 to-blue-100 container white">
      <div class="heading ml-10"><h3>Data Identification Information</h3></div>
     <div class="flex justify-start">
       <div class="">
        <label for="nom" class="mr-28">Name of Dataset</label><br />
        <div class="">
          <input type="text" class="w-full h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" :value="subtheme" readonly /><i
            class="fa-solid fa-circle-check"
            id="tick-nom"
          ></i>
        </div>
      </div>
     </div>
      <div class="flex justify-start items-start">
        <div class="theme">
        <label for="theme" class="mr-48" >Theme</label><br />
        <input type="text" class="w-full h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" :value="theme" readonly /><i
          class="fa-solid fa-circle-check"
          id="tick-theme"
        ></i>
      </div>
      </div>
      <div class="flex justify-start">
        <div class="keywords">
        <label class="mr-96">Keywords</label> <br />
        <div class="boxes">
          <!-- <div class="row-one">
          <input type="text" class="keyword-box" id="firstbox" v-model="KeywordOne"> <i class="fa-solid fa-circle-check" id="tick-box-1" v-if="CorrectKeywordOne && KeywordOne"  ></i>
          <i
          id="cross-1"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectKeywordOne && KeywordOne"
        ></i>
          <input type="text" class="keyword-box" id="secondbox" v-model="KeywordTwo"><i class="fa-solid fa-circle-check" id="tick-box-2" v-if="CorrectKeywordTwo && KeywordTwo"></i>
          <i
          id="cross-2"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectKeywordTwo && KeywordTwo"
        ></i>
          <input type="text" class="keyword-box" id="thirdbox" v-model="KeywordThree"><i class="fa-solid fa-circle-check" id="tick-box-3"  v-if="CorrectKeywordThree && KeywordThree"></i>
          <i
          id="cross-3"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectKeywordThree && KeywordThree"
        ></i>
          <input type="text" class="keyword-box" id="fourthbox" v-model="KeywordFour"><i class="fa-solid fa-circle-check" id="tick-box-4" v-if="CorrectKeywordFour&& KeywordFour"></i>
          <i
          id="cross-4"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectKeywordFour && KeywordFour"
        ></i>
        </div>
        <div class="row-two">
          <input type="text" class="keyword-box" id="firstbox2" v-model="KeywordOneOne"><i class="fa-solid fa-circle-check" id="tick-box-5"  v-if="CorrectKeywordOneTwo && KeywordOneOne"></i>
          <i
          id="cross-5"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectKeywordOneOne && KeywordOneOne"
        ></i>
          <input type="text" class="keyword-box" id="secondbox2" v-model="KeywordOneTwo"><i class="fa-solid fa-circle-check" id="tick-box-6"  v-if="CorrectKeywordOneTwo && KeywordOneTwo"></i>
          <i
          id="cross-6"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectKeywordOneTwo && KeywordOneTwo"
        ></i>
          <input type="text" class="keyword-box" id="thirdbox2" v-model="KeywordOneThree"><i class="fa-solid fa-circle-check" id="tick-box-7" v-if="CorrectKeywordOneThree && KeywordOneThree"></i>
          <i
          id="cross-7"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectKeywordOneThree && KeywordOneThree"
        ></i>
          <input type="text" class="keyword-box" id="fourthbox2" v-model="KeywordOneFour"><i class="fa-solid fa-circle-check" id="tick-box-8"  v-if="CorrectKeywordOneFour && KeywordOneFour"></i>
          <i
          id="cross-8"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectKeywordOneFour && KeywordOneFour"
        ></i>
        </div>-->
          <div class="keyword-row">
            <div
              v-for="(keyword, index) in firstRowKeywords"
              :key="index"
              class="keyword-box"
            >
              <input
                type="text"
                v-model="keyword.value"
                class="h-10 w-8 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-6 box-border"
                @input="checkDuplicate(keyword, index, 'firstRowKeywords')"
              />
              <i v-if="keyword.value && !keyword.duplicate" class="fa-solid fa-circle-check valid"></i>
              <i v-else-if="keyword.value && keyword.duplicate" class="fa-solid fa-circle-xmark invalid"></i>
            </div>
          </div>
          <div class="keyword-row">
            <div
              v-for="(keyword, index) in secondRowKeywords"
              :key="index"
              class="keyword-box"
            >
              <input
                type="text"
                v-model="keyword.value"
                class=" h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border"
                @input="checkDuplicate(keyword, index, 'secondRowKeywords')"
              />
              <i v-if="keyword.value && !keyword.duplicate" class="fa-solid fa-circle-check valid"></i>
              <i v-else-if="keyword.value && keyword.duplicate" class="fa-solid fa-circle-xmark invalid"></i>
            </div>
          </div>
        </div>
      </div>
      </div>
      <div class="flex justify-start">
        <div class="access-constraints">
        <label for="ac-cs" class="mr-20">Access Constraints</label><br />
        <input type="text" class="ac h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" v-model="AccessConstraint" @input="ValidateAccessConstraints"/>
        <i
          class="fa-solid fa-circle-check"
          id="tick-ac-cs"
          v-if="CorrectAccessConstraints && AccessConstraint"
        ></i>
        <i
          id="cross-ac-cs"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectAccessConstraints && AccessConstraint"
        ></i>
      </div>
      </div>
      <div class="flex justify-start"> 
        <div class="use-constraints">
        <label for="use-cs" class="mr-24">Use-Constraints</label> <br />
        <input type="text" class="ac h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" v-model="UseConstraints" @input="ValidateUseConstraints"/><i
          class="fa-solid fa-circle-check"
          id="tick-use-cs"
          v-if="CorrectUseConstraints && UseConstraints"
        ></i>
        <i
          id="cross-use-cs"
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectUseConstraints && UseConstraints"
        ></i>
      </div>
      </div>
      <div class="flex justify-start">
        <div class="purpose">
        <label for="purpose" class="mr-5"
          >Purpose of creating data</label
        ><br />
        <input type="text" class="ac h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" v-model="Purpose" @input="ValidatePurpose" /><i
          class="fa-solid fa-circle-check"
          
          v-if="CorrectPurpose && Purpose"
        ></i>
        <i
          
          class="fa-solid fa-circle-xmark"
          v-if="!CorrectPurpose && Purpose"
        ></i>
      </div>
      </div>
      <div class="bottom">
        <div class="data-type">
          <label for="dataType">Data Type</label><br />
          <select name="data-type" id="dataType" v-model="dataType" class="w-36 h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border">
            <option value="Vector_Data">Vector Data</option>
            <option value="Raster_Data">Raster Data</option>
          </select>
        </div>
        <div class="Edition">
          <label for="edition">Edition</label><br />
          <select name="edition" id="edition" v-model="edition" class="w-36 h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border">
            <option value="first">First</option>
            <option value="second">Second</option>
          </select>
        </div>
        <div class="Status">
          <label for="status">Status</label><br />
          <select name="status" id="status" v-model="status" class="w-36 h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border">
            <option value="completed">Completed</option>
            <option value="in progress">In Progress</option>
          </select>
        </div>
      </div>
    </div>
    <div class="bottom-layer">
    <div class="steps">
      <span id="current-step">2</span> of <span id="total-steps">12</span>
    </div>
    <div class="move-icons">
      <i class="fa-solid fa-circle-chevron-left" id="left" @click="handleLeftClick"></i>
      <i
        id="right"
        class="fa-solid fa-circle-chevron-left"
        @click="handleRightClick"
      ></i>
    </div>
  </div>
  </div>
</template>

<script>
import { ref, watch } from "vue";
import useValidate from "@vuelidate/core";

export default {
  props: ["subtheme", "theme"],
  setup(props, { emit }) {
    
    const CorrectNameOfDataset = ref(true);
    const firstRowKeywords = ref([
      { value: "", duplicate: false },
      { value: "", duplicate: false },
      { value: "", duplicate: false },
      { value: "", duplicate: false },
    ]);

    const secondRowKeywords = ref([
      { value: "", duplicate: false },
      { value: "", duplicate: false },
      { value: "", duplicate: false },
      { value: "", duplicate: false },
    ]);

    // const CorrectTheme = ref(true);
  
    // const CorrectKeywordOne = ref(false);
    // const KeywordOne = ref("");
    // const CorrectKeywordTwo = ref(true);
    // const KeywordTwo = ref("");
    // const CorrectKeywordThree = ref(true);
    // const KeywordThree = ref("");
    // const CorrectKeywordFour = ref(true);
    // const KeywordFour = ref("");
    // const CorrectKeywordOneOne = ref(true);
    // const KeywordOneOne = ref("");
    // const CorrectKeywordOneTwo = ref(true);
    // const KeywordOneTwo = ref("");
    // const CorrectKeywordOneThree = ref(true);
    // const KeywordOneThree = ref("");
    // const CorrectKeywordOneFour = ref(true);
    // const KeywordOneFour = ref("");
    const status = ref("");
    const edition = ref("");
    const dataType = ref("");
    const CorrectAccessConstraints = ref(false);
    const AccessConstraint = ref("");
    const v$ = useValidate();
    const CorrectUseConstraints = ref(false);
    const UseConstraints = ref("");
    const CorrectPurpose = ref(false);
    const Purpose = ref("");

    const handleRightClick = () => {
      // const { emit } = getCurrentInstance(); // Access emit function using getCurrentInstance
      // Emit an event to the parent component to validate and proceed
      // Ensure that the necessary data is filled
     
        // Emit an event to the parent component
        // This event is caught in the parent component to proceed to the next step

        const data = {
        
        AccessConstraint: AccessConstraint.value,
        CorrectAccessConstraints: CorrectAccessConstraints.value,
        UseConstraints: UseConstraints.value,
        CorrectUseConstraints: CorrectUseConstraints.value,
        Purpose: Purpose.value,
        CorrectPurpose: CorrectPurpose.value,
        firstRowKeywords: firstRowKeywords.value,
        secondRowKeywords: secondRowKeywords.value,
        dataType: dataType.value,
        edition: edition.value,
        status: status.value,
        
        
      };
      // Emit the 'update-data' event with the updated data
      emit("update-data", data);

        emit('validate-and-proceed-second-form');
        console.log('emiteed');
       
      
    };
    
    const handleLeftClick = () =>{
      emit('MoveBackToExtra')
    }

    //Check Access COnstraint Length is < 100
    const ValidateAccessConstraints= ()=>{
      CorrectAccessConstraints.value = AccessConstraint.value.length < 100;
    } 

    // Watch for changes in AccessConstraint
    watch(AccessConstraint, () => {
      ValidateAccessConstraints();
    });
    

    //Check USe COnstraint Length is < 100
    const ValidateUseConstraints= ()=>{
      CorrectUseConstraints.value = UseConstraints.value.length < 100;
    } 
    
    // Watch for changes in USeConstraint
    watch(UseConstraints, () => {
      ValidateUseConstraints();
    });

    //Check Access COnstraint Length is < 100
    const ValidatePurpose= ()=>{
      CorrectPurpose.value = Purpose.value.length < 200;
    } 

    // Watch for changes in AccessConstraint
    watch(AccessConstraint, () => {
      ValidateAccessConstraints();
    });
   

    // Function to check for duplicate keywords
    const checkDuplicate = (keyword, rowIndex, rowType) => {
      if (!keyword.value) {
    keyword.duplicate = false; // Reset duplicate flag if input is empty
    return;

    
  }

  const rowKeywords = rowType === 'firstRowKeywords' ? firstRowKeywords.value : secondRowKeywords.value;
  const allKeywords = [...firstRowKeywords.value, ...secondRowKeywords.value];
  const allValues = allKeywords.map(item => item.value.toLowerCase());

  const currentIndex = rowIndex + (rowType === 'secondRowKeywords' ? firstRowKeywords.value.length : 0);
  const currentValue = keyword.value.toLowerCase();
  const isDuplicate = allValues.filter((item, index) => index !== currentIndex && item === currentValue).length > 0;

  keyword.duplicate = isDuplicate;

  // Check for duplicates across both rows
  if (isDuplicate) {
    alert('Keywords must be different.');
  }
    };

    // Return variables to be used in the component
    return {
      
      ValidateAccessConstraints,
      ValidatePurpose,
      checkDuplicate,
      handleLeftClick,
      secondRowKeywords,
      firstRowKeywords,
      CorrectAccessConstraints,
      CorrectUseConstraints,
      CorrectPurpose,
      Purpose,
      AccessConstraint,
      UseConstraints,
      v$,
      status,
      edition,
      dataType,
      handleRightClick, 
    };
  },
};
</script>


<style scoped>
i {
  z-index: 999;
}

.ac{
  width: 185%;
}

body {
  padding: 0;
  margin: 0;
}

.bottom {
  display: flex;
  /* align-items: center; */
  justify-content: space-evenly;
  gap: 25px;
}

#cross-nom {
  color: crimson;
  position: relative;
  right: 190px;
}
#cross-theme {
  color: crimson;
  position: relative;
  right: 105px;
}

.keyword-rows {
  display: flex;
  flex-direction: column;
}

.keyword-row {
  display: flex;
  justify-content: space-between;
}

.keyword-box {
  width: calc(25% - 10px); /* Adjust as needed */
  position: relative;
}

.keyword-box input {
  width: 100%;
}

/* Add styles for valid and invalid icons */
.valid {
  color: green;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  right: 10px;
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


.invalid {
  color: crimson;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  right: 10px;
}

#tick-theme {
  color: green;
  position: relative;
  right: 105px;
}

#tick-nom {
  color: green;
  position: relative;
  right: 190px;
}

#tick-box-1,
#tick-box-5 {
  color: green;
  position: absolute;
  top: 15px;
  left: 125px;
}
#tick-box-2,
#tick-box-6 {
  color: green;
  position: absolute;
  top: 15px;
  left: 273px;
}
#tick-box-3,
#tick-box-7 {
  color: green;
  position: absolute;
  top: 15px;
  left: 419px;
}
#tick-box-4,
#tick-box-8 {
  color: green;
  position: absolute;
  top: 15px;
  left: 561px;
}

#tick-purpose,
#tick-use-cs,
#tick-ac-cs {
  color: green;
  position: relative;
  right: 37px;
}

#right {
  transform: rotate(180deg);
  position: relative;
  left: 5px;
}

#cross-1,
#cross-5 {
  color: crimson;
  position: absolute;
  top: 15px;
  left: 125px;
}
#cross-2,
#cross-6 {
  color: crimson;
  position: absolute;
  top: 15px;
  left: 273px;
}
#cross-3,
#cross-7 {
  color: crimson;
  position: absolute;
  top: 15px;
  left: 419px;
}
#cross-4,
#cross-8 {
  color: crimson;
  position: absolute;
  top: 15px;
  left: 561px;
}

#cross-purpose,
#cross-use-cs,
#cross-ac-cs {
  color: crimson;
  position: relative;
  right: 37px;
}

h1 {
  margin: 0;
}
.form-container-two {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-bottom: 100px;
}

.white-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 10px;

  border-radius: 56px;
  background: linear-gradient(
    180deg,
    #b2e2f1,
    rgba(178, 226, 241, 0.5) 99.99%,
    rgba(178, 226, 241, 0)
  );
  box-shadow: 0px 4.4px 4.42px rgba(0, 0, 0, 0.25);
  backdrop-filter: blur(9.18px);
  box-sizing: border-box;
  padding: 35px 27px 37px 25px;
  max-width: 100%;
}

 

.heading {
  position: relative;
  right: 163px;
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

.themelabel {
  position: relative;
  right: 260px;
}

h3{
  padding: 0;
  margin: 0;
  position: relative;
  left: 25px;
  padding-bottom: 12px;
}

.keyword-heading {
  position: relative;
  right: 250px;
}

.ac-cs {
  position: relative;
  right: 217px;
}

.use-cs {
  position: relative;
  right: 227px;
}

.heading-purpose {
  position: relative;
  right: 194px;
}

  


.boxes {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.row-one {
  position: relative;
  right: 16px;
}
.row-two {
  position: relative;
  right: 16px;
}




input,
select {
  margin-top: 5px;
}

/* Base styles */

/* Styles for small phones (portrait and landscape) */
@media only screen and (max-width: 480px) {
  /* Your CSS rules for small phones */
  h3{
    font-size: 15px;
    left: 135px;
  }
  .nom,.themelabel,.keyword-heading,.ac-cs,.use-cs,.heading-purpose{
    font-size: 15px;
    right: 100px;
  }
  .nom{
    right: 75px;
  }
  .heading-purpose{
    right: 55px;
  }
  .ac-cs{
    right: 75px;
  }
  .white-container{
    padding: 35px 2px 37px 25px;
  }

  .use-cs{
    right: 85px;
  }
  #tick-theme,#tick-nom{
    right: 45px;

  }
  .theme input{
    width: 257px;
    right: 20px;
  }
  .keywords input{
    width: 130px;
    margin-left: 0;
  }
  .keyword-row{
    justify-content: flex-start;
    gap: 2px;
  }
.keyword-box{
  width: 135px;
}
.access-constraints input{
  width: 300px;
  right:10px ;
}

.use-constraints input{
  width: 300px;
  right: 10px;
}

.boxes{
  flex-direction: row;
}

.keyword-row{
  flex-direction: column;
}

.purpose input{
   width: 300px;
  right: 10px;
}

.name-of-dataset input{
  right: 20px;
}

#tick-ac-cs,#tick-purpose,#tick-use-cs{
  right: 34px;
}

.bottom{
  flex-direction: column;
  gap: 5px;
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

}

</style>
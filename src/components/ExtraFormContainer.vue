<template>
  <div class="bottom-layer">
    <div class="steps">
      <span class="bg-gradient-to-r from-blue-100 to-blue-100 p-3.5 py-2 rounded-xl">2</span> of <span id="total-steps">12</span>
    </div>
    <div class="move-icons">
      <i
        class="fa-solid fa-circle-chevron-left"
        id="left"
        @click="handleLeftClick"
      ></i>
      <i
        id="right"
        class="fa-solid fa-circle-chevron-left"
        @click="handleRightClick"
      ></i>
    </div>
  </div>
  <div class="flex flex-col gap-5 rounded-3xl drop-shadow-md backdrop-blur box-border p-7 bg-gradient-to-r from-blue-100 to-blue-100 container white">
    <div class="flex gap-16">
      <label class="font-semibold text-xl mt-2" for="extension">Extension</label>
      <select name="extension"  class="w-full h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" v-model="extension">
        <option value="jp2">.jp2</option>
        <option value="tif">.tif</option>
      </select>
    </div>
    <div class="flex gap-8">
      <label for="compression" class="font-semibold text-xl mt-2">Compression</label>
      <select name="compression"  class="w-full h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" v-model="Compression">
        <option value="jp2000">jp2000</option>
        <option value="deflate">deflate</option>
      </select>
    </div>
    <div class="flex gap-12">
      <label for="resampling" class="font-semibold text-xl mt-2">Resampling</label>
      <select name="compression" class="w-full h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" v-model="resampling">
        <option value="Nearest">Nearest</option>
        <option value="Mode">Mode</option>
        <option value="average">Average</option>
      </select>
    </div>
    <div class="flex gap-16">
      <label for="interleave" class="font-semibold text-xl mt-2">Interleave</label>
      <select name="interleave" class="w-full h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border" v-model="interleave">
        <option value="pixel">Pixel</option>
      </select>
    </div>

    <div class="flex gap-10">
      <label for="projection" class="font-semibold text-xl mr-5 mt-2">Projection</label>
      <div class="flex gap-2 ">
        <div class="first flex">
          <input @input="validateProjections"
            type="text"
            id="projection"
            class=" w-24 h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border"
            v-model="Projection"
          />
          <i
            class="fa-solid fa-circle-check"
            id="tick"
            v-if="CorrectProjectOne && Projection"
          ></i>
          <i
            id="cross"
            class="fa-solid fa-circle-xmark"
            v-if="!CorrectProjectOne && Projection"
          ></i>
        </div>

        <button class="py-2 px-4 bg-blue-500 hover:bg-blue-600 text-white font-semibold rounded-lg shadow-md focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75 mr-56" v-if="!showProjection2" @click="addInput">Add</button>
        <div class="second">
          <input
            type="text"
            id="projection"
            class=" w-24 h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border"
            v-model="Projection2"
            v-show="showProjection2"
          />
          <i
            class="fa-solid fa-circle-check"
            id="tick"
            v-show="CorrectProjectTwo && Projection2"
          ></i>
          <i
            id="cross"
            class="fa-solid fa-circle-xmark"
            v-show="!CorrectProjectTwo && Projection2"
          ></i>
        </div>
        <button class="py-2 px-4 bg-blue-500 hover:bg-blue-600 text-white font-semibold rounded-lg shadow-md focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75 mr-56" v-show="!showProjection3 && showProjection2" @click="addInput2">
          Add
        </button>
        <div class="third">
          <input
            type="text"
            id="projection"
            class=" w-24 h-10 rounded-3xl bg-blue-50 shadow-md border-none text-base p-4 pr-11 box-border"
            v-model="Projection3"
            v-show="showProjection3"
          />
          <i
            class="fa-solid fa-circle-check"
            id="tick"
            v-show="CorrectProjectThree && Projection3"
          ></i>
          <i
            id="cross"
            class="fa-solid fa-circle-xmark"
            v-show="!CorrectProjectThree && Projection3"
          ></i>
        </div>
      </div>
    </div>
  </div>
  
  <input
    type="hidden"
    :value="subtheme"
    @input="updateSubtheme($event.target.value)"
  />
  <input
    type="hidden"
    :value="theme"
    @input="updateTheme($event.target.value)"
  />
</template>

<script>
import { ref, watch } from "vue";
import useValidate from "@vuelidate/core";

export default {
  /*
  // data() {
  //   return {
  //     v$: useValidate(),
  //     Correctprojections: false,
  //     extension: "",
  //     Compression: "",
  //     projection: "",
  //   };
  // },
  validations() {
    return {
      extension: { required },
      Compression: { required },
      projection: { required },
    };
  },
  methods: {
    validateprojections() {
      this.Correctprojections = this.projection.startsWith("/");
    },
  */
  props: ["subtheme", "theme"],

  setup(props, { emit }) {
    const extension = ref("");
    const interleave = ref("");
    const Compression = ref("");
    const Projection = ref("");
    const Projection2 = ref("");
    const Projection3 = ref("");
    const showProjection3 = ref(false);
    const showProjection2 = ref(false);
    const resampling = ref("");
    const Correctprojections = ref(false); // Initial validation
    const CorrectProjectOne = ref(false);
    const CorrectProjectTwo = ref(false);
    const CorrectProjectThree = ref(false);
    const Projectionarray = ref([]);
    const paused = ref(false);
    const temporal_frequency = ref("daily");
   const validateProjections = () => {
     Projectionarray.value = []; 
  if (Projection.value.trim() !== "") {
    Projectionarray.value.push(Projection.value);
  }
  if (Projection2.value.trim() !== "") {
    Projectionarray.value.push(Projection2.value);
  }
  if (Projection3.value.trim() !== "") {
    Projectionarray.value.push(Projection3.value);
  }
};

    const v$ = useValidate();
    function addInputWrapper() {}

    const addInput = () => {
      showProjection2.value = true;
    };
    
    const addInput2 = () => {
      showProjection3.value = true;
    };

    const updateSubtheme = (value) => {
      this.$emit("update:subtheme", value);
    };
    const updateTheme = (value) => {
      this.$emit("update:theme", value);
    };

    const validateProjection = () => {
      CorrectProjectOne.value =
        Projection.value !== Projection2.value &&
        Projection.value !== Projection3.value;
      CorrectProjectTwo.value =
        Projection2.value !== Projection.value &&
        Projection2.value !== Projection3.value;
      CorrectProjectThree.value =
        Projection3.value !== Projection.value &&
        Projection3.value !== Projection2.value;

      if (
        (!CorrectProjectOne.value ||
          !CorrectProjectTwo.value ||
          !CorrectProjectThree.value) &&
        Projection.value.trim() !== "" &&
        Projection2.value.trim() !== "" &&
        Projection3.value.trim() !== ""
      ) {
        alert(
          "Please ensure that the projections are different from each other."
        );
      }
    };

    watch(Projection, validateProjection);
    watch(Projection2, validateProjection);
    watch(Projection3, validateProjection);

    const handleRightClick = () => {
      
      // Emit an event to the parent component to validate and proceed
      validateProjections();

      // Emit an event to the parent component
      // This event is caught in the parent component to proceed to the next step
      console.log(Projectionarray.value);
     
      emit(
        "validate-and-proceed",
        subtheme.value,
        theme.value,
        
      );
      const data = {
        subtheme: props.subtheme,
        theme: props.theme,
        extension: extension.value,
        Compression: Compression.value,
        Projection: Projection.value,
        Projection2: Projection2.value,
        Projection3: Projection3.value,
        CorrectProjectOne: CorrectProjectOne.value,
        CorrectProjectTwo: CorrectProjectTwo.value,
        CorrectProjectThree: CorrectProjectThree.value,
        resampling: resampling.value,
        interleave: interleave.value,
        projection: Projectionarray.value,
        paused : paused.value,
        temporal_frequency: temporal_frequency.value,
      };
      // Emit the 'update-data' event with the updated data
      emit("update-data", data);
       
   
    };

    const handleLeftClick = () => {
      emit("MoveBackToOne");
    };

    return {
      extension,
      handleLeftClick,
      updateSubtheme,
      updateTheme,
      CorrectProjectOne,
      CorrectProjectThree,
      CorrectProjectTwo,
      Projection2,
      Projection3,
      addInput2,
      Compression,
      addInput,
      Projection,
      Correctprojections,
      addInputWrapper,
      showProjection2,
      showProjection3,
      validateProjection,
      handleRightClick,
      v$,
      interleave,
      resampling,
      validateProjections,
      paused,
      temporal_frequency,
    };
  },
};
</script>

<style scoped>

.white{
  width: 520px;
  
}

.projection{
  position: relative;
}
body {
  margin: 0;
  padding: 0;
  height: 100%;
}

.form-container-extra {
  display: flex;
  flex-direction: column;
  gap: 20px;
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
  padding: 35px 27px 37px 44px;
  max-width: 100%;
}


#tick {
  color: green;
  position: absolute;
  z-index: 999;
  right: 9px;
  top: 12px;
}
#cross {
  color: crimson;
  position: absolute;
  z-index: 999;
  right: 10px;
  top: 12px;
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

.extensionText,
.compressionText,
.resamplingText,.interleaveText {
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
.interleave{
  display: flex;
  gap: 45px;
}

#extension,
#compression,
#resampling,
#interleave {
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
}

#interleave{
  position: relative;
  left: 9px;
}

#resampling{
  position: relative;
  right: 13px;
}

#compression{
  margin-left: 6px;
}

.projection input {
  width: 139px; /* Adjust as needed */
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
  margin-left: 8px;
}

.inputs {
  display: flex;
  gap: 8px;
  justify-content: space-between;
  position: relative;
  left: 174px;
}



.compression,
.extension {
  display: flex;
  gap: 10px;
}

.resampling {
  display: flex;
  gap: 50px;
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

.extension {
  gap: 52px;
}

.form-container-extra {
  display: flex;
  flex-direction: column;
}


.input-wrapper {
  display: flex;
  align-items: center;
}

.add-button {
  width: 120px; /* Adjust the width as needed */
  margin-top: 10px;
}


/* Base styles */

/* Styles for small phones (portrait and landscape) */
@media only screen and (max-width: 480px) {
  /* Your CSS rules for small phones */
  .form-container-extra{
    padding: 30px 20px 30px 20px;
  }

  .compressionText,.resamplingText,.extensionText,.interleaveText{
    font-size: 18px;
  }

  #extension,#interleave,#compression,#resampling{
    width: 150px;
    height: 31px;
  }
  .ProjectionText{
    left: 20px;
    font-size: 18px;
  }
  .inputs{
    left: 155px;
    gap: 3px;
  }
  .projection input{
    margin-top: 5px;
    height: 32px;
    width: 59px;
  }
  button{
    min-width: 12px;
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

<template>
  <div class="scrollbar" :style="{ backgroundColor: backgroundColor }">
    <div class="left-scroll" @click="scrollToLeft">
      <img src="../assets/left-arrow.png" alt="left-arrow" />
    </div>
    <div class=" container mx-auto justify-between container-1 flex overflow-x-auto" ref="container">
      <div class="primary-data-management h-72 bg-blue-100 rounded-3xl p-5">
        <h3 class=" font-semibold">Primary Data Management</h3>
        <p class="pdm-text">
          Lorem ipsum cing elit, sed eiusmod tem incididunt
        </p>
        <span @click="$router.push('/Primary-data-main-page')"><button class="get-started-pdm btn">Get Started</button></span>
      </div>
      <div class="Shard-Management bg-blue-100  rounded-3xl p-4">
        <h3 class=" font-semibold">Shard <br> Management</h3>
        <p class="pdm-text">
          Lorem ipsum cing elit, sed eiusmod tem incididunt
        </p>
        <span ><button class="get-started-sm btn" >Get Started</button></span>
      </div>
      <div class="Pyramind-Management bg-blue-100 rounded-3xl p-4">
        <h3 class=" font-semibold">Pyramind <br> Management</h3>
        <p class="pdm-text">
          Lorem ipsum cing elit, sed eiusmod tem incididunt
        </p>
        <span><button class="get-started-pym btn">Get Started</button></span>
      </div>
      <div class="Pool-Management bg-blue-100 rounded-3xl p-4">
        <h3 class=" font-semibold">Pool <br> Management</h3>
        <p class="pdm-text">
          Lorem ipsum cing elit, sed eiusmod tem incididunt
        </p>
        <span><button class="get-started-pom btn">Get Started</button></span>
      </div>
      <div class="Registry-Management bg-blue-100 rounded-3xl p-4">
        <h3  class=" font-semibold">Registry Management</h3>
        <p class="pdm-text">
          Lorem ipsum cing elit, sed eiusmod tem incididunt
        </p>
        <span><button class="get-started-rm btn">Get Started</button></span>
      </div>
      <div class="any1-Management bg-blue-100 rounded-3xl p-4">
        <h3 class=" font-semibold">Any1 <br> Management</h3>
        <p class="pdm-text">
          Lorem ipsum cing elit, sed eiusmod tem incididunt
        </p>
        <span><button class="get-started-a1m btn  ">Get Started</button></span>
      </div>
    </div>
    <div class="right-scroll" @click="scrollToRight">
      <img src="../assets/left-arrow.png" alt="left-arrow" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    backgroundColor: {
      type: String,
      default: "transparent",
    },
    scrollDistance: {
      type: Number,
      default: 100,
    },
  },
  methods: {
    scrollToLeft() {
      const container = this.$refs.container;
      container.scrollTo({
        left: container.scrollLeft - container.offsetWidth,
        behavior: "smooth",
      });
    },
    scrollToRight() {
      const container = this.$refs.container;
      container.scrollTo({
        left: container.scrollLeft + container.offsetWidth,
        behavior: "smooth",
      });
    },
  },
};
</script>

<style scoped>
.scrollbar {
  position: relative;
  display: flex;
  background-color: transparent;
  gap: 20px;
  position: relative;
  padding: 20px;
  justify-content: center;
  text-shadow: none;
}

.btn{
  margin-top: 20px;
}

.left-scroll img,
.right-scroll img {
  margin-top: 115px;
  width: 44px;
  height: 50px;
}

.scrollbar span {
  padding: 20px;
}

.scrollbar button {
  height: 52px;
  width: 133px;
  position: relative;
  border-radius: 30px;
  border: none;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  font-size: 17px;
  font-style: italic;
}

.pdm-text {
  width: 120px;
  margin-left: 27px;
  margin-top: 15px;
}

.left-scroll,
.right-scroll {
   position: absolute; /* Position the scroll buttons absolutely */
    
  
  cursor: pointer;
}

.left-scroll {
  left: 0; /* Adjust the left position as needed */
}

.right-scroll {
  right: 0; /* Adjust the right position as needed */
  transform: rotate(180deg);
  margin-top: 120px;
}

.container-1 {
  display: flex;
  gap: 20px;
  overflow-x: auto;
  padding: 10px;
  width: 81%;
}

.container-1::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

button {
  cursor: pointer;
}

/* Media Queries */
@media screen and (max-width: 640px) {
  /* Small mobile devices */
  .container-1 {
    width: 16.8%;
  }
  .left-scroll {
    left: 38%;
  }
  .right-scroll {
    right: 38%;
  }

}

@media screen and (min-width: 641px) and (max-width: 767px) {
  /* Big mobile devices */
  .container-1 {
    width: 71%;
  }
   .left-scroll {
    left: 10%;
  }
  .right-scroll {
    right: 10%;
  }
}

@media screen and (min-width: 768px) and (max-width: 1023px) {
  /* Small laptops and tablets */
  .container-1 {
    width: 59%;
  }
  .left-scroll {
    left: 15%;
  }
  .right-scroll {
    right: 15%;
  }
}

@media screen and (min-width: 1024px) and (max-width: 1279px) {
  /* Big laptops and desktops */
  .container-1 {
    width: 66%;
  }
  .left-scroll {
    left: 14%;
  }
  .right-scroll {
    right: 13%;
  }
}
@media screen and (min-width: 1280px) and (max-width: 1440px) {
  /* Big laptops and desktops */
  .container-1 {
    width: 71%;
  }
  .left-scroll {
    left: 11%;
  }
  .right-scroll {
    right: 12%;
  }
}
@media screen and (min-width: 1441px) {
  /* Big laptops and desktops */
  .container-1 {
    width: 79%;
  }
  .left-scroll {
    left: 3%;
  }
  .right-scroll {
    right: 3%;
  }
}
</style>

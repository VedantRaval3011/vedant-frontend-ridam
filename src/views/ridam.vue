<template class="h-screen w-screen">
  <div class="main flex flex-col gap-1 w-screen h-screen bg-gradient-to-b from-blue-300 to-blue-200 overflow-hidden">
    <div class="flex justify-between p-4">
      <div class="flex items-center">
        <img src="../assets/vedas.png" alt="vedas logo" class="w-16 h-auto" />
      </div>
      <div class="flex items-center">
        <img src="../assets/userbg.png" alt="user-image" class="w-16 h-16 rounded-full shadow-md" />
      </div>
    </div>
    <div class="flex flex-col items-center justify-center flex-1">
      <h1 class="text-4xl font-bold mb-2">RIDaM</h1>
      <div class="flex flex-col items-center mb-4">
        <button @click="$router.push('/')"
          class="py-2 px-4 bg-blue-500 hover:bg-blue-600 text-white font-semibold rounded-lg shadow-md focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75 mr-56" >
          Back
        </button>
        <div class="pill bg-blue-100 rounded-full p-3 shadow-md mt-3">
          <p class="text-lg font-semibold">Raster Analytics System for Interactive Data Modeling</p>
        </div>
      </div>
      <h2 class="text-xl font-semibold mb-4">Select the management module</h2>
      <ScrollableModule scrollDistance="3000" />
    </div>
    <div class="flex justify-end p-4 bg-blue-100">
      <p class="text-lg font-medium">About RIDaM</p>
    </div>
  </div>
</template>

<script>
import ScrollableModule from "../components/ScrollableModule.vue";
export default {
  name: "Ridam",
  components: {
    ScrollableModule,
  },
};
</script>

<!-- No scoped styles needed, as Tailwind CSS is utility-based -->
<style scoped>
  /* Media Queries */
@media screen and (max-width: 640px) {
  /* Small mobile devices */
 

}

@media screen and (min-width: 641px) and (max-width: 767px) {
  /* Big mobile devices */
 
}

@media screen and (min-width: 768px) and (max-width: 1023px) {
  /* Small laptops and tablets */
 
}

@media screen and (min-width: 1024px) and (max-width: 1279px) {
  /* Big laptops and desktops */
  
}
@media screen and (min-width: 1280px) and (max-width: 1440px) {
  /* Big laptops and desktops */

}
@media screen and (min-width: 1441px) {
  /* Big laptops and desktops */

}
</style>
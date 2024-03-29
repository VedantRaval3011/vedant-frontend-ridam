<template>
  <div class="bg-gradient-to-b from-blue-300 to-blue-200 min-h-screen flex flex-col justify-between">
    <div class="flex justify-between items-center py-4 px-6">
      <div class="logo">
        <img src="../assets/vedas.png" alt="vedas logo" class="h-20" />
      </div>
      <div class="login">
        <button class="btn text-sm"><span>LOGIN</span></button>
      </div>
    </div>
    <div class="flex flex-col justify-center items-center">
      <h1 class="text-3xl text-center text-custom-text font-semibold drop-shadow-2xl">Vedas Geo-spatial Dataset Management System</h1>
      <div class="flex mt-8">
        <button class="ridam btn mr-4">
          <router-link to="/ridam" class="ridamrouter">RIDaM</router-link>
        </button>
        <button class="geo-entity-state-system btn" disabled>Geo-entity Stats System</button>
      </div>
    </div>
    <div class="pb-4 bg-gray-100 pt-2 text-pretty">
      <p class="help-manual text-right cursor-pointer" @click="$router.push('/AboutView')">Help-manual</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
};
</script>

<style scoped>


.text-custom-text {
  color: #344747;
}

.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 9999px;
  background: linear-gradient(to bottom, #c3e5f9, #c3e5f9);
  color: #344747;
  font-size: 16px;
  font-style: italic;
  box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.2);
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.login-button {
  width: 80px;
}

.help-manual {
  margin-right: 26px;
  font-weight: 450;
  color: #344747;
}
</style>

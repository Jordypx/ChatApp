<template>

<div v-if="state.username === '' || state.username === null" class="flex justify-center w-full mt-40">
  <form @submit.prevent="Login" class="bg-white shadow-md rounded px-20 pt-20 pb-20 mb-4 m-16">
   <div class="mr-16">
     <h1 class="text-4xl mb-10">Login to whatsapp</h1>
    <label for="username" class="block text-gray-700 font-bold mb-2 text-2xl">Username</label>
    <input type="text" class="shadow appearance-none border rounded w-full py-4 px-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mb-10 text-xl" v-model="inputUsername" placeholder="Enter your username...">
    <!-- <input type="submit" value="Login"> -->

    <div class="flex items-center justify-between">
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-6 rounded focus:outline-none focus:shadow-outline" type="submit">
        LogIn
      </button>
      <a class="inline-block align-baseline font-bold text-xl text-blue-500 hover:text-blue-800" href="#">
        Forgot Username?
      </a>
    </div>
   </div>
  </form>
</div>



<div v-else>
   <!-- <chat/> -->
    <preloader/>
</div>

</template>

<script>
// import db from './db'  
import { reactive, ref} from 'vue';
// import chat from "../components/chat.vue"
import preloader from '../components/preloader.vue'


export default {
  name: 'login',

  setup () {
     const inputUsername = ref("");

     const state = reactive({
      username: "",
      messages: []
     });

     const Login = () => {
      if (inputUsername.value != "" || inputUsername.value !=null) {
         state.username = inputUsername.value;
         inputUsername.value = "";
      }
     } 

     return {
      inputUsername,
      Login,
      state
     }
  },

  components: {
   // chat,
   preloader,
  },

}

</script>

<style>
</style>

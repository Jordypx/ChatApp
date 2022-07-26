<template>
<transition>
   <div v-if="show" class="flex flex-col items-center justify-center absolute w-full h-full bg-white z-9999 ease-out duration-300">
       <div class="mb-24"><img class="w-56" src="../assets/whatsapp-logo-png-2259.png" alt="whatsapp"></div>
   </div>
</transition>

<div> 
    <chatbody/>
</div>

</template>




<script>
// import chat from "../components/chat.vue"
import chatbody from '../components/chatbody.vue'

export default {
   name: 'preloader',
   data() {
      return {
         show: true
      }
   },
   mounted(){
     this.showToggle()
   },
   methods: {
      showToggle(){
         setTimeout(() => {
               this.show = false
         }, 6000)
      }
   },

  components: {
    chatbody,
  },
   
}
</script>



<style scoped>


</style>
<template>
<transition>
   <div v-if="show" class="flex flex-col items-center justify-center absolute w-full h-full bg-white z-9999 ease-out duration-300">
       <div class="mb-24"><img class="w-56" src="../assets/whatsapp-logo-png-2259.png" alt="whatsapp"></div>
   </div>
</transition>

<div></div>

</template>




<script>
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
   }
   
}
</script>



<style scoped>


</style>
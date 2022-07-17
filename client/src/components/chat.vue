<template>

<div>
  <preloader/>
</div>

<div>
  <chatbody/>
</div>

</template>





<script>
import preloader from '../components/preloader.vue'
import chatbody from '../components/chatbody.vue'


export default {
   name: "chat",

   components: {
    preloader,
    chatbody,
   }

}




</script>







<style>



</style>
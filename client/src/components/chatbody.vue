<template class="sm">

<div class="flex justify-between bg-green-600 p-4 text-lg font-bold text-white w-full m-0">
   <header class="">WhatsApp</header>

   <!-- <div class="btn">
      <button type="submit" class="text-2xl text-center">Logout</button>
   </div> -->
</div>


  <div class="container flex max-w-full bg-white shadow">
       
    <!-- left_side -->


    <div class="left bg-white">
        <div class="w-full h-24 bg-gray-100 flex justify-between items-center p-2.5 border-r-2">
               
         <div class="user-image w-16 rounded cursor-pointer overflow-hidden">
            <img class="rounded-full h-16 w-full" src="../assets/2213426.jpg" alt="m">
         </div>


         <ul class="flex">
               <li class="flex text-sm list-none cursor-pointer ml-8"><img class="w-7 text-gray-200" src="../assets/scan-circle-outline_1.svg" alt=""></li> 
               <li class="flex text-sm list-none cursor-pointer ml-8"><img class="w-7 text-gray-200" src="../assets/plus-large.svg" alt=""></li>
               <li class="flex text-sm list-none cursor-pointer ml-8"><img class="w-7 text-gray-200" src="../assets/ellipsis.svg" alt=""></li>
            </ul>
        </div>


        <div class="relative w-full flex justify-center items-center">
               
                <div class="w-full flex justify-center items-center border-b-2">

                  <input class="w-full bg-gray-200 h-16 rounded-xl text-xl pl-16 m-4 outline-0 border-0" type="text" placeholder="Search or start new chat">

                   <div><img class="w-7 absolute left-8 bottom-8" src="../assets/NicePng_magnifying-glass-png-no_659698.png" alt=""></div>
               
                </div>
            
            </div>



<!-- chat-list -->

             <div class="chatlist">
               <div class="flex w-full p-3 border-b-2 items-center cursor-pointer justify-around bg-gray-100">
                  <div class="imgbox rounded cursor-pointer overflow-hidden ">
                     <img class="rounded-full h-16 w-20" src="../assets/jeffery-erhunse-Z9lbmEjyYjU-unsplash.jpg" alt="">
                  </div>
                  <div class="details w-full relative ml-6">
                     <div class="listhead flex justify-between mb-2">
                        <h4 class="text-2xl font-semibold">Grace</h4>
                        <p class="text-lg text-green-400">11:47</p>
                     </div>
                     <div class="message_p flex justify-between ">
                        <p class="text-xl overflow-hidden text-ellipsis font-medium">how are you doing?</p>

                        <b class="text-count bg-green-400 text-white flex justify-center items-center h-8 p-3 text-center left-3">3</b>
                     </div>
                  </div>
               </div>

         </div>


      </div>



     <!-- Right-side -->

     <div class="right">

      <div class="right-header w-full h-24 bg-gray-100 flex justify-between p-4">

         <div class="img-text flex justify-center">
                        <div class="userimg">
                           <img class="rounded-full h-16 w-16" src="../assets/jeffery-erhunse-Z9lbmEjyYjU-unsplash.jpg" alt="">
                        </div>
                        <h4 class="font-medium leading-7 ml-3 text-2xl p-1.5 text-gray-600">Grace<br><span class="text-lg text-gray-500">online</span></h4>
                     </div>

         <ul class="flex">
               <li class="flex text-sm list-none cursor-pointer ml-8"></li> 
               <li class="flex text-sm list-none cursor-pointer ml-8"><img class="w-7 h-7 m-4" src="../assets/NicePng_magnifying-glass-png-no_659698.png" alt=""></li>
               <li class="flex text-sm list-none cursor-pointer ml-8"><img class="w-7 text-gray-200" src="../assets/ellipsis.svg" alt=""></li>
            </ul>
      </div>


           <!-- chat-box -->

       <div class="chatbox w-full">
                  <div class="message my_message flex w-full" v-for="message in messages" :key="message.id">
                     <div class="message my_message flex w-full" v-if="message.id % 2 == 0">
                        <p class="">{{ message.message}}</p>
                     </div>

                  <div class="message frnd_message flex w-full" v-else>
                      <p class="message bot"> {{ message.message}}</p>
                  </div>
               </div>

                 
               </div>


          <!-- chat input -->

               <div class="input-chat flex w-full p-1 justify-around items-center bg-gray-100 ">
                  <div class="smile-img pl-9">

                     <img class="w-11  cursor-pointer" src="../assets/emoticon-24-256.png" alt="">

                  </div>

                  <div class="attach pl-9">

                     <img class="w-11  cursor-pointer" src="../assets/attach-2-256.png" alt="">

                  </div>

                  <form class="flex justify-center w-full" @submit.prevent="sendMessage()">
                      <input v-model="messageContent" id='createMessage' class="text-input w-11/12 m-3 p-5 rounded-lg text-2xl" type="text" placeholder="Type a message">

                       <div>
                        <img class="send-btn w-10 cursor-pointer"  src="../assets/documentsend_104490.png" alt="" type="submit" @click="sendMessage()">
                       </div>
                  </form>
               

                  <!-- <div class="send">

                     <img class="w-12 mr-12 cursor-pointer"  src="../assets/documentsend_104490.png" alt="" type="submit">
                  
                  </div> -->

               </div>
     </div>

  </div>



<!-- </div>

</div> -->



</template>







<script>
import axios from 'axios';
import { ref } from "vue";

// const data = {
//    message: "do you want to know my name",
// };

// axios.post("http://localhost:8000/chat", data).then((res) => console.log(res.data));

export default {
   name: 'chatbody',

   setup() {
      const messages = ref([]),
       messageContent = ref("");

      function sendMessage() {
         if(messageContent.value == "") return

         createMessage(messageContent.value);
         getResponse(messageContent.value);
         messageContent.value = ""
      }


      function createMessage(message) {
         let id = 0;
         if (messages.value[messages.value.length -1]) {
            id = messages.value[messages.value.length -1].id + 1;
         }
         messages.value.push({
            id:id,
            message:message,
         })
      }

      async function getResponse(message) {
         const postData = {
            message: message,
         };
         const {data} = await axios.post("http://localhost:8000/chat", postData)
         const {response} = data
         createMessage(response);

      }

      return { messages, messageContent, sendMessage}
   },


}



</script>
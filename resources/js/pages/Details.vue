<template>
<div class="w-full flex px-6">
  <div id="Details" class="flex-grow px-2">
    <div class="header py-4 flex justify-between items-center border-b-2">
      <div>
        <h2 class="text-xl font-bold text-green-500"><i class="pi pi-calendar px-2"></i>Todo 01</h2>
      </div>
      <div class="flex flex-row items-center">
        <img src="/img/three.svg" />
        <span><i class="pi text-green-500 px-4 pi-user-plus" /></span>
      </div>
    </div>
    <div class="sub-header flex py-3 items-center border-b-2">
      <div class="button px-4 py-2 mr-2 bg-green-500 font-bold cursor-pointer rounded text-white">+ Add a new Task</div>
      <div class="amt_completed px-4 py-2 flex items-center">
        <svg width="19" height="19" viewBox="0 0 19 19" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M10.9999 1.82458H4.99988C4.17145 1.82458 3.49988 2.49616 3.49988 3.32459V15.3246C3.49988 16.153 4.17145 16.8246 4.99988 16.8246H13.9999C14.8283 16.8246 15.4999 16.153 15.4999 15.3246V6.32459L10.9999 1.82458Z" stroke="#242424" stroke-width="1.22693" stroke-linecap="round" stroke-linejoin="round"/>
        <path d="M10.9999 1.82458V6.32459H15.4999" stroke="#242424" stroke-width="1.22693" stroke-linecap="round" stroke-linejoin="round"/>
        <path d="M12.4999 10.0747H6.49988" stroke="#242424" stroke-width="1.22693" stroke-linecap="round" stroke-linejoin="round"/>
        <path d="M12.4999 13.0747H6.49988" stroke="#242424" stroke-width="1.22693" stroke-linecap="round" stroke-linejoin="round"/>
        <path d="M7.99988 7.07458H7.24988H6.49988" stroke="#242424" stroke-width="1.22693" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
<!-- 07060961923 -->
        <span class="font-bold ">3 completed</span>
      </div>
    </div>
    <div class="description py-2 ">
      <span>Our todo plugin is a collection which means more than one todo can be made. Each todo can contain multiple tasks containing which includes: the title, the description, list of check able task. Note each todo is a room, when you create a todo you’ve automatically created a channel with the  same name (visible in the side bar) and everyone assigned to it will be in that channel. At the point of creating the todo you can decide to make it private or public </span>
    </div>
    <div class="progress_container flex flex-col">
      <span class="progress_text self-end text-sm font-medium ">100% Completed</span>
      <progress id="progress" class="w-full mx-auto" :value="percent" max="100"> 32% </progress>
    </div>
    <div class="tasks_container py-4">
      <span class="task_head font-bold my-2">Pending</span>
      <div v-for="(i, index) in alltasks" :key="index++" class="pl-4 m-2 task_box flex py-2 hover:shadow rounded hover:border">
        <Checkbox v-model="checked" :id="'city' + index++" name="city" :value="'Chicago' + index++" />
        <div class="task_content flex-grow pl-2">
          <p class="task_title pb-3 font-medium"><span class="task_number">Task 0{{index++}} -</span> in the main todo, every intern must complete a task succesfully to go to stage 6</p>
          <div class="task_details flex flex-row justify-between">
            <div class="task_comment-amt flex items-center">
              <img src="/img/three.svg"/>
              <span class="pl-2 font-bold text-sm text-green-500">5 comments</span>
              <span class="pl-2 text-gray-500 text-sm">Last Comment 12 hours ago</span>
            </div>
            <div class="task_tag flex flex-row items-center">
              <div class="text-gray-500 pr-1"><i class="pi pi-tag"></i><span class="px-2 capitalize font-bold text-sm">General</span></div>
              <div class="text-gray-500 pr-1"><i class="pi pi-tag"></i><span class="px-2 capitalize font-bold text-sm">HNG</span></div>
              <div class="text-blue-500 pr-1"><i class="pi pi-calendar"></i><span class="px-2 font-bold text-sm">Tomorrow</span></div>
              <div></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div id="Comment" class="w-1/4 flex-shrink-0 border"></div>
    <!-- <div class="flex flex-row justify-between items-center"> 
      {{this.$route.params.id}}
      <div @click="close" class="font-bold text-green-500">X</div>
      </div>
      <p class="text-green-500 font-bold ">
        This is the todo details section,
        
      </p>
      <p class="text-lg font-bold text-wrap text-red-500">Still under construction</p> -->
      <!-- <div>
        <div>
          <p>Task Title</p>
        <span>Created On: 12/03348n/39424</span>
        <p>oihsoiv hwt0pu;n4wy0iohjgwklef</p>
        </div>
        <div>
          <p>Task Title</p>
          <div>
            
          </div>
        </div>
        <div class="flex">
          <div>
            <p>Due Date</p>
            <span>p320409</span>
          </div>
          <div>
            <p>Worked </p>
            <span>loiwheot</span>
          </div>
        </div>
      </div> -->
      <!-- <TextArea /> -->
    </div>
   
</template>
<script>
import Checkbox from 'primevue/checkbox';
import TextArea from '../components/TextArea.vue'
import CommentBox from '../components/CommentBox.vue'
import {mapGetters} from 'vuex'
export default {
    name: 'TodoDetails',
    data(){
      return {
        selectedTodo: '',
        checked: [],
        alltasks: ['','','','','','','','','','']
      }
    },
        computed: {
      ...mapGetters({
        allTodos: 'todos/allTodos'
      }),
      percent(){
       return (this.checked.length / this.alltasks.length) * 100
      }
    },
    components: {
      TextArea,
      Checkbox
    },
  methods: {
    close(){
      this.$emit('hideComment')
    },
    check(){
      let id = this.$route.params.id
      this.selectedTodo = this.allTodos.find( todo => todo.card_id.toLowerCase() === (id.toLowerCase()));
       if(this.selectedTodo <= 0 || this.selectedTodo === undefined){
         this.$emit('hideComment')
         this.$router.push({path: '/main'})
         
       }
       else {
       }
      console.log(this.selectedTodo)
    },
    
  },
  mounted(){
      // this.check();
    }
}
</script>
<style lang="scss">
progress[value] {
  /* Reset the default appearance */
  -webkit-appearance: none;
   appearance: none;
  border-radius: .6em;
  height: 5px;
  //  box-shadow: 0 0 10px rgb(0 103 69 / 28%);
}
progress[value]::-webkit-progress-bar {
 
  border-radius: 2px;
  background-color: #E2ECF8;
}
progress[value]::-webkit-progress-value {
  background-color: #00B87C;
  border-radius: 2px;
}
</style>

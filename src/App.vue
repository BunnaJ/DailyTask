<template>
  <div class="container">
    <div class="main">
  <div class="header">
    <h1>  Daily Task</h1>
    <i class="fa-solid fa-list-check"></i>

  </div>
  <div class="display">
    <textarea type="text" required v-model="inputValue"></textarea>
    <button @click="addItem">Add</button>
  </div>
  <div v-for="item in taskItems" :key="item.id" class="items">
    <input type="checkbox" v-model="item.checked">
    <p>{{item.text }}</p>
    <span><i class="fa-solid fa-trash"  @click="removeItems(item.id)"></i></span>
  </div>

  <Error v-show="error.show" :message="error.message" @close="closeErrorDialog"/>

</div>
  </div>
</template>

<script>
import Error from "./components/ErrorDialog.vue";

export default {
  data()  {
    return {
      inputValue:'',
      taskItems: [],
      error: {
        message: '',
        show: false,
      },
      
    }
  },
  components: {Error},

  mounted(){
    //  let items = localStorage.getItem('todoList');
    //  if(items)  this.taskItems = JSON.parse(items);

    this.taskItems = localStorage.getItem('todoList') ? 
      JSON.parse(localStorage.getItem('todoList')) : 
      [];
  },

  methods: {
    addItem() {
        if(this.inputValue.trim() == '') return;

        let items = [...this.taskItems];
        let value = this.inputValue.trim();

         items.push({
            id: 'td'+Date.now(),
            text: value,
            checked: false,
         });
         this.taskItems = items;
         this.inputValue = '';
         this.saveTodo();
    },

    removeItems(id) {
      // let items = [...this.taskItems];
      let checked = false;
      this.taskItems.forEach(item => {
        if(item.id == id){
          checked = item.checked;
        }
      });

      if(checked){
        this.taskItems = this.taskItems.filter(item => {
          return !item.checked;
        }) 
        
        this.error = {
          show: false,
          message: '',
        }

        this.saveTodo();

      }else{
        let error = {...this.error};
        error.show = true;
        error.message = 'hey🖐️! complete your daily task, then check, to be able to delete thank you and stay disciplined 🥸' ;
        this.error = error;
      }
           
    },
    closeErrorDialog(value){
      // let error = {...this.error};
      // error.show = false;
      // error.message = '';
      // this.error = error;
      this.error = {
        show: false,
        message: '',
      }
    },

    saveTodo(){
      localStorage.setItem('todoList', JSON.stringify(this.taskItems));
    }
  },

}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Alumni+Sans+Collegiate+One:ital@1&family=Lato&family=Nunito:wght@600;900&family=Playfair+Display:ital@1&family=Poppins:wght@200;400;500;600;700&family=Roboto+Condensed:wght@700&family=Rubik+Bubbles&family=Rubik+Maps&display=swap');
  body{
    height: 100vh;  
     background-image: url('./assets/daily1.avif'); 
    background-repeat: repeat;
    background-size: 100%;
    background-position: cover;
  }

.container{
    background-image: url('./assets/daily2.webp'); 
    background-repeat: repeat;
    background-size: 100%;
    background-position: cover;

  max-width: 1000px; 
   margin: 0 auto; 
   margin-top: 200px; 
   border-radius: 20px; 

}
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
   background: rgba(0, 0 , 0, 0.5);
   border-radius: 10px;

}
.header{
  display: flex;
  align-items: center;
  justify-content: center;
}
.header h1{
  font-family: rubik maps;
  color: #ddd;
}
.header i {
  font-size: 40px;
  padding-left: 20px;
  color: #fff;
}
.display{
  display: flex;
  width: 50%;
  margin-top: 10px;
  padding-bottom: 20px;
}
.display textarea{
  outline: none;
  border: none;
  width: 80%;
  font-family: lato;
  color: #000;
  
}
.display button{
  background: #ff5c5c;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;

}
.items{
  background: rgb(168, 158, 158);
  width: 50%;
  margin-top: 2px;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  border-radius: 5px;
   animation: slideIn 350ms ;
   margin-bottom: 20px;
}
.items p {
  width: 80%;
  overflow-wrap: break-word;
  line-height: 25px;

}
@keyframes slideIn {
  50% {
    transform: translateY(30%);
  }
}
.task_holder{
  display: flex;
  align-items: center;
}
.task_holder input{
  margin-left: 10px;
}
textarea{
  padding: 10px 20px;
}
.items i {
  font-size: 20px;
  margin-right: 10px;
  color: #000;
 
}


/* /////// */
@media screen and (max-width:680px) {
  .display{
    display: flex;
    width: 95%;
  }
 
  .items{
    width: 95%;
    overflow: hidden;
  }
  .main{
    border-radius: 5px;
  }
  .display button{
    color: black;
  }

}
</style>
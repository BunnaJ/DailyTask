<template>
<div class="contain">
  <div class="modal">
    <p>{{message}}</p>
     <span @click="$emit('close', true)"><i class="fa-solid fa-xmark"></i></span>
  </div>
</div>
</template>

<script>
export default {
    props: ['message'],
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Alumni+Sans+Collegiate+One:ital@1&family=Exo+2:wght@300&family=Lato&family=Nunito:wght@600;900&family=Playfair+Display:ital@1&family=Poppins:wght@200;400;500;600;700&family=Roboto+Condensed:wght@700&family=Rubik+Bubbles&family=Rubik+Maps&display=swap');

.modal {
  display: flex;
  width: 400px;
  padding: 20px;
  margin: 20% auto;
  background: #a08787;
  border-radius: 10px;
  top: 10px;
  position:relative;
  justify-content: space-between;
  animation: slideIn 1s;
  color: #ddd;
  font: Exo 2;

}
@keyframes slideIn {
  50% {
    transform: translateY(30%);
  }
}
.contain{
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}
.modal span i{
  position: absolute;
  top: 0;
  font-size: 20px;
  margin-right: 40px;
  color: rgb(33, 34, 34);
  
}

@media screen and (max-width:680px) {
  .modal {
    width: 80%;
    margin-top: 30%;
  }
  .contain{
    width: 100%;
    top: 0;
  }
}
</style>
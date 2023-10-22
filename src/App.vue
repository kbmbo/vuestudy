<template>
  <SliderBom />
<!--  <div class="gnb">-->
<!--    <ul>-->
<!--      <li v-for="i in menu" :key="i">{{i}}</li>-->
<!--    </ul>-->
<!--  </div>-->
<!--  <Banner />-->
<!--  <div class="container">-->
<!--    <RoomList  v-for="(obj, i) in products" :key="i" @click="modal(obj.id)" :products="obj" />-->
<!--  </div>-->
<!--  <Modal :modalState="modalState" />-->
</template>

<script>
import rooms from '@/data/services.js'
// import Banner from "@/components/Banner";
// import Modal from "@/components/Modal";
// import RoomList from "@/components/RoomList";
import SliderBom from "@/components/Slide";
import '@/assets/css/slider.scss'

export default {
  name: 'App',
  data(){
    return {
      menu: ['Home','Products','About'],
      products : rooms,
      modalState: {open: false, data: null},

    }
  },
  methods: {
    modal(id){
      this.modalState.open = !this.modalState.open
      id !== undefined ? this.products.map(obj => {
        if(obj.id == id){
          this.modalState.data = obj;
        }
      }) : this.modalState.data = null;
    }
  },
  components: {
    // RoomList,
    // Modal,
    // Banner,
    SliderBom
  }
}
</script>

<style>
body {margin: 0; padding: 0;}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
ul {list-style: none;}
.gnb {border-bottom: 1px solid #2c3e50; margin-bottom: 30px;}
.gnb ul{
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
.gnb li{cursor : pointer}

.container{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
}

</style>

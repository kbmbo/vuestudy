<template>
  <div class="gnb">
    <ul>
      <li v-for="i in menu" :key="i">{{i}}</li>
    </ul>
  </div>
  <div class="container">
    <div class="list" v-for="(obj, i) in products" :key="i">
      <div class="img" v-bind:style="{backgroundImage: `url(${obj.image})`}"></div>
      <h4 @click="modal(obj.id)">{{obj.title}}</h4>
      <p>보증금 {{obj.price}}원</p>
      <p>{{obj.content}}</p>
      <button @click="clickCount(i)">허위 매물 신고</button>
      <span>{{obj.count}} 건</span>
    </div>
  </div>
  <div class="modalContainer" v-if="modalOpen !== false">
    <div class="dim">
      <div class="contents" v-if="modalData !== null">
        <div class="x-btn"><button @click="modal()">X</button></div>
        <h4>{{modalData.title}}</h4>
        <div>
          <div class="img" v-bind:style="{backgroundImage: `url(${modalData.image})`}"></div>
          <p>{{modalData.content}}</p>
          <p>{{modalData.price}}원</p>
        </div>
      </div>
      <div v-else><p>상세내용이 없습니다.</p></div>
    </div>
  </div>

<!--  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import rooms from './data/services.js'

export default {
  name: 'App',
  data(){
    return {
      menu: ['Home','Products','About'],
      products : rooms,
      modalOpen: false,
      modalData: null
    }
  },
  methods: {
    clickCount(i){
     this.products[i].count += 1
    },
    modal(id){
      this.modalOpen = !this.modalOpen
      id !== undefined ? this.products.map(obj => {
        if(obj.id == id){
          this.modalData = obj;
        }
      }) : this.modalData = null;
    }
  },
  components: {
    //HelloWorld
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
.gnb {border-bottom: 1px solid #2c3e50; margin-bottom: 50px;}
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
.list {width: 30%; margin-bottom: 20px}
.list button{ margin-right: 5px; }
.img {
  width: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  aspect-ratio: 1.65;
}
.modalContainer {
  position: fixed;
  top: 0;
}
.modalContainer .dim {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0,0,0,.6);
}
.modalContainer .contents {
  width: 60%;
  background-color: #fff;
  border-radius: 10px;
}
.modalContainer .x-btn {
  display: flex;
  justify-content: flex-end;
}
</style>

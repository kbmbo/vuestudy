<template>
  <div class="modalContainer" v-if="modalState.open !== false">
    <div class="dim">
      <div class="contents" v-if="modalState.data !== null">
<!--        <div class="x-btn"><button @click="modal()">X</button></div>-->
        <h4>{{modalState.data.title}}</h4>
        <div>
          <div class="img" :style="{backgroundImage: `url(${modalState.data.image})`}"></div>
          <p>{{modalState.data.content}}</p>
          <p>{{modalState.data.price}}원</p>
        </div>
        <Banner />
      </div>
      <div v-else><p>상세내용이 없습니다.</p></div>
    </div>
  </div>
</template>

<script>
 export default {
   // eslint-disable-next-line vue/multi-word-component-names
   name: 'Modal',
   props: {
     modalState: Object
   },
   methods: {
   },
 }
</script>

<style>
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
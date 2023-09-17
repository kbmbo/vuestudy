<template>
  <div class="list">
    <div class="img" :style="{backgroundImage: `url(${products.image})`}"></div>
    <h4>{{products.title}}</h4>
    <p>보증금 {{products.price}}원</p>
    <p>{{products.content}}</p>
    <button @click="clickCount()">허위 매물 신고</button>
    <span>{{count}} 건</span>
  </div>
</template>

<script>
  export default {
    name: 'RoomList',
    data() {
      return {
        count : this.products.count
      }
    },
    props: {
      products: Object
    },
    methods: {
      clickCount(){
        this.count += 1
      },
    },
  }
</script>

<style>
  .list {width: 30%; margin-bottom: 20px}
  .list button{ margin-right: 5px; }
  .img {
    width: 100%;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    aspect-ratio: 1.65;
  }
</style>
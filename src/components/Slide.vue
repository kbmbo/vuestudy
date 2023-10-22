<template>
  <div class="host-slider"
          v-if="cache.companyResponse?.posters !== null && cache.companyResponse?.posters.length > 1">
    <div class="slide-view slideView" :class="cache.companyResponse?.posters.length === 2 && 'two'" @touchstart="sliderChanged">
      <div class="panel-wrap">
        <div v-for="(poster, i) in cache.companyResponse?.posters" :key="poster.priority" class="panel">
          <div class="imgWrap">
            <p>{{ i }}</p>
            <img :src="poster.posterImg.filePath" @click="detailPoster(poster)" :alt="poster.posterImg.fileName"/>
          </div>
        </div>
      </div>
    </div>
    <div class="nav-warp">
      <button class="prev" @click="navClick"></button>
      <button class="next" @click="navClick"></button>
    </div>

  </div>
<!--  <div class="poster-popup" v-show="this.showPoster">-->
<!--    <div class="poster-popup_content" v-if="popupPoster.posterImg !== null">-->
<!--      <image-comp :image="popupPoster.posterImg" width ratio='2/3' />-->
<!--      <div class="btn-warp">-->
<!--        <button>닫기 X</button>-->
<!--        <button>바로가기 ></button>-->
<!--      </div>-->
<!--    </div>-->
<!--  </div>-->
</template>

<script>
  export default {
    name: 'SliderBom',
    data() {
      return {
        cache: {
          companyId: undefined,
          companyResponse: {
            posters: [
              {
                linkUrl:"srt",
                posterImg: {
                  fileName:"신규가입.png",
                  filePath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/19/20698/8d04fd25-f411-412d-824c-a56e179dbec0_30db5cad-89b1-4ae6-b10a-9ed1f6fb7621_신규가입.png",
                  thumbnailPath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/19/20698/8d04fd25-f411-412d-824c-a56e179dbec0_thumb_30db5cad-89b1-4ae6-b10a-9ed1f6fb7621_신규가입.png"
                },
                priority:0,
                publicStat:"PRIVATE"
              },
              {
                linkUrl:"https://bootstrap-vue.org/docs/icons",
                posterImg:{
                  fileName:"14697703983668[1].jpg",
                  filePath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/20/20698/4d518396-9f7d-40ea-98d3-06c4249aff73_3fa8d42f-944c-467b-a2cb-01f3208ffcdb_14697703983668[1].jpg",
                  thumbnailPath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/20/20698/4d518396-9f7d-40ea-98d3-06c4249aff73_thumb_3fa8d42f-944c-467b-a2cb-01f3208ffcdb_14697703983668[1].jpg"
                },
                priority:2,publicStat:"PUBLIC"
              },
              {
                linkUrl:"https://bootstrap-vue.org/docs/icons",
                posterImg: {
                  fileName:"Mask group.jpg",
                  filePath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/20/20698/27ad6c58-9ef4-4fab-b4be-3c33170b0e20_1b317366-5669-4014-a5b2-95143c42d8aa_Mask group.jpg",
                  thumbnailPath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/20/20698/27ad6c58-9ef4-4fab-b4be-3c33170b0e20_thumb_1b317366-5669-4014-a5b2-95143c42d8aa_Mask group.jpg"
                },
                priority:1,
                publicStat:"PRIVATE"
              },
              {
                linkUrl:"https://bootstrap-vue.org/docs/icons",
                posterImg: {
                  fileName:"5991dcf9a7d1cecditem_32.jpg",
                  filePath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/20/20698/f5b626b5-7769-43e5-b198-0f31f78dfa5f_be46a395-f49e-477a-835e-b12a2857ffdb_5991dcf9a7d1cecditem_32.jpg",
                  thumbnailPath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/20/20698/f5b626b5-7769-43e5-b198-0f31f78dfa5f_thumb_be46a395-f49e-477a-835e-b12a2857ffdb_5991dcf9a7d1cecditem_32.jpg"
                },
                priority:3,
                publicStat:"PUBLIC"
              },
              {
                linkUrl:"https://bootstrap-vue.org/docs/icons",
                posterImg: {
                  fileName:"5991dcf9a7d1cecditem_32.jpg",
                  filePath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/20/20698/f5b626b5-7769-43e5-b198-0f31f78dfa5f_be46a395-f49e-477a-835e-b12a2857ffdb_5991dcf9a7d1cecditem_32.jpg",
                  thumbnailPath:"https://cdn.pokerpass.io/local/pokerpass/images/2023/10/20/20698/f5b626b5-7769-43e5-b198-0f31f78dfa5f_thumb_be46a395-f49e-477a-835e-b12a2857ffdb_5991dcf9a7d1cecditem_32.jpg"
                },
                priority:3,
                publicStat:"PUBLIC"
              }
            ]
          },
          eventList: [],
          follow: undefined,
        },
      }
    },
    methods: {
      sliderChanged(e) {
        console.log(e);
      },
      navClick(e){
        const panelWrap = document.querySelector('.panel-wrap');
        const panel = panelWrap.children;
        if (e.target.className === 'next'){
          Array.from(panel).forEach( (el, i) => {
            el.classList.remove('slide-prev', 'slide-active', 'slide-next')
            i == 1 && el.classList.add('slide-prev');
            i == 2 && el.classList.add('slide-active');
            i == 3 && el.classList.add('slide-next');
          })
          panelWrap.style.transform =`translate3d(-15%, 0, 0)`;
        }
      },
      detailPoster(poster) {
        console.log('zmfflr');
        this.popupPoster = {
          posterImg: poster.posterImg,
          linkUrl: poster.linkUrl
        }
        this.showPoster = true
      },
    },
    mounted() {
      const slideViewW = getComputedStyle(document.querySelector('.slideView')).width
      const panelWrap = document.querySelector('.panel-wrap');
      const panel = panelWrap.children;
      const total= this.cache.companyResponse?.posters.length+2

      const firstChild = panelWrap.firstElementChild;
      const lastChild = panelWrap.lastElementChild;
      const clonedFirst = firstChild.cloneNode(true);
      const clonedLast = lastChild.cloneNode(true);
      panelWrap.insertAdjacentHTML('afterbegin', clonedLast.outerHTML);
      panelWrap.insertAdjacentHTML('beforeend', clonedFirst.outerHTML);
      panelWrap.style.width = `calc((${slideViewW}/2) *${total})`

      Array.from(panel).forEach( (el, i) => {
        el.style.width = `calc(${slideViewW}/2)`
        i == 0 && el.classList.add('slide-prev');
        i == 1 && el.classList.add('slide-active');
        i == 2 && el.classList.add('slide-next');
      })
    }
  }
</script>
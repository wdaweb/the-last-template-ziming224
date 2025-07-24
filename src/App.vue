<template>
  <v-app>
    <v-app-bar style="background: #5FB38B;">
      <v-container class="d-flex align-center">
        <v-app-bar-title>番茄鐘</v-app-bar-title>
        <v-btn prepend-icon="mdi-home" to="/">首頁</v-btn>
        <v-btn prepend-icon="mdi-format-list-bulleted" to="/list">事項</v-btn>
        <v-btn prepend-icon="mdi-cog" to="/settings">設定</v-btn>
      </v-container>
    </v-app-bar>
    <v-main>


  <swiper :pagination="true" :modules="modules" class="mySwiper">
    <swiper-slide v-for="(img,index) in imgs" :key="index">
      <img :src="img" style="cursor: pointer;" @click="openLightbox(index)"/></swiper-slide>
  </swiper>

  <EasyLightbox
  :visible="visible"
  :imgs="imgs"
  :index="index"
  @hide="visible = false"
/>



        <img
        ref="tomato"
        src="../—Pngtree—cute tomato icon_7276272.png"
        alt="番茄"
        style="width: 100px; position: absolute; left: 0; bottom: 80px;"
      />
      <!--
      <SlotExample v-slot="apple">
        <h1>{{ apple }}</h1>
        <h1>{{ apple.num }}</h1>
        <h1>{{ apple.text }}</h1>
      </SlotExample>
      <SlotExample v-slot="{ num }">
        <h1>{{ num }}</h1>
      </SlotExample>
      -->
      <!--
      <CardA />
      <component :is="CardA" />
      <component :is="CardB" />
      <component :is="c" v-for="(c, i) in components" :key="i" />
      -->
      <!--
        slot = 插槽 = 自訂元件內的某部分 HTML
        v-slot="插槽提供的元件內的變數"
        https://zh-hk.vuejs.org/guide/components/slots.html#scoped-slots
        Component = 目前路由應該顯示的元件
        https://router.vuejs.org/zh/guide/advanced/router-view-slot.html#RouterView-%E6%8F%92%E6%A7%BD
      -->
      <router-view v-slot="{ Component }">
        <!--
          keep-alive 包住的元件不會被銷毀
          include 指定保留的元件
          https://zh-hk.vuejs.org/guide/built-ins/keep-alive.html#include-exclude
        -->
        <!--
          component 動態元件
          is 要使用的元件
        -->
        <keep-alive include="HomeView">
          <component :is="Component" />
        </keep-alive>
      </router-view>
    </v-main>
  </v-app>
</template>


<style>
.v-main {
  background-color:#58708A !important;
}
</style>


<script setup>

      // return {
      //   modules: [Pagination],
      // };
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination } from 'swiper/modules';
import 'swiper/css'
import 'swiper/css/pagination'
import { ref, onMounted } from 'vue'
import gsap from 'gsap'
import EasyLightbox from 'vue-easy-lightbox'

// Swiper 模組
const modules = [Pagination]

// 番茄 DOM
const tomato = ref(null)

// Lightbox 狀態
const visible = ref(false)
const index = ref(0)

const openLightbox = (i) => {
  index.value = i
  visible.value = true
}

// 番茄動畫
onMounted(() => {
  gsap.to(tomato.value, {
    x: 1800, // 左右移動
    rotation: 720 , // 同時旋轉
    duration: 5,
    repeat: -1, // 無限循環
    yoyo: true, // 來回
    ease: 'power1.inOut',
  })
})

// Swiper 輪播的圖片
const imgs = [
  'https://picsum.photos/1900/200/?random=1',
  'https://picsum.photos/1900/200/?random=2',
  'https://picsum.photos/1900/200/?random=3',
  'https://picsum.photos/1900/200/?random=4',
  'https://picsum.photos/1900/200/?random=5',
]

// import CardA from '@/components/CardA.vue'
// import CardB from '@/components/CardB.vue'
// import SlotExample from '@/components/SlotExample.vue'

// const components = [CardA, CardB]
</script>

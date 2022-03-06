<script setup lang="ts">
import { ref, onMouted } from "vue";
import axios from "axios";

const url = ref("");

const showDog = () => {
   axios.get(
    "https://dog.ceo/api/breeds/image/random"
  ).then((res)=>{
    url.value = res.data.message;
  })
};
</script>

<template>
  <button v-on:click="showDog">ワンワン</button>
  <div>
    <img :src=url />
  </div>
</template>

<script setup lang="ts">
import { ref, onUpdated } from "vue";
import axios from "axios";

const address = ref("");
const postcode = ref("");

onUpdated(async () => {
  const zipcode = postcode.value;
  if (zipcode.length !== 7) return;

  const response = await axios.get(
    `https://zipcloud.ibsnet.co.jp/api/search?zipcode=${zipcode}`
  );
  address.value = response.data.results[0].address3;
});
</script>

<template>
  <input v-model="postcode" id="textBox" />
  <p>住所: {{ address }}</p>
</template>

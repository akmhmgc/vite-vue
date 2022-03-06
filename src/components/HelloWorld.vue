<script setup lang="ts">
import { ref, onMounted, onUpdated } from "vue";
import axios from "axios";

defineProps<{ msg: string }>();

const count = ref(0);
const msg = ref("");
const address = ref("");
const postcode = ref("");

const add = (): void => {
  count.value += 1;
};

onUpdated(async () => {
  const zipcode = postcode.value;
  if (zipcode.length !== 7) return;

  await axios
    .get(`https://zipcloud.ibsnet.co.jp/api/search?zipcode=${zipcode}`)
    .then((response) => {
      address.value = response.data.results[0].address3;
    });
});
</script>

<template>
  <button type="button" @click="add" id="count">count is: {{ count }}</button>
  <input v-model="postcode" id="textBox" />
  <p>住所: {{ address }}</p>
</template>
g
<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>

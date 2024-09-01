<template>
  <button @click="getNewImage">Get Image</button>
  <img class="imgContainer" :src="image?.urls?.raw" />
</template>

<script setup>
import { ref, onMounted } from 'vue'
// import { utility } from '../utility/utility';
import { createApi } from "unsplash-js";

defineProps({
  msg: String,
})

const splashApi = createApi({
  // Don't forget to set your access token here!
  accessKey: "sfXJzi9uH2kLucq4iVysRSSzH7FF7XDFEBugoYt1uas"
})

const image = ref();

onMounted(() => {
  getNewImage();
})

function getNewImage() {
  splashApi.photos
    .getRandom({ topics:"hints,events,street,location,places,streetview,india",query: "city+streets", orientation: "landscape", perPage: 1,})
    .then(result => {
      image.value = result.response;
    })
    .catch(() => {
      console.log("something went wrong!");
    })
}


</script>

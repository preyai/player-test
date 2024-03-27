<script setup>
import {PlayerFactory} from "rbt-player/dist"
import {onMounted, ref, watch} from "vue";
const player = ref(null)
const video = ref(null)
const url = ref("https://fl3.lanta.me:8443/121358")
const token = ref("8f30fc67f68ad45736731f506b132f958c602b8a-a42fbd07119abae9db209f7da788e4b1-1711548677-1711537877")
const date = ref(null)
// test
watch([url,token],() => {
  console.log('22')
  player.value?.onDestroy()
  player.value = PlayerFactory.createPlayer({
    camera: {
      serverType: 'flussonic',
      url: url.value,
      token: token.value
    },
    videoElement:video.value,
    autoplay: true,
  })
})
watch(date,() => {
  // console.log()
  player.value.generateStream(new Date(date.value).getTime()/1000, 60*60)
})
onMounted(() => {
  player.value = PlayerFactory.createPlayer({
    camera: {
      serverType: 'flussonic',
      url: url.value,
      token: token.value,

    },
    videoElement:video.value,
    autoplay: true,
  })
})
</script>

<template>
  <div class="card">
  <input v-model="url" placeholder="url" />
  <input v-model="token"  placeholder="token"/>
    <input type="datetime-local" v-model="date" />
  <video ref="video" class=""/>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 24px;
  max-width: 90%;
  video {
    width: 100%;
    height: 100%;
  }
}
</style>
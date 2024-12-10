<script setup lang="ts">
import {ref,computed} from "vue"
import {artistData} from "./artists.js"
import {songsData} from "./songs.js"
import {Artist} from "./models/artist.ts"
import {Song} from "./models/song.ts"
import Main from "./views/Main.vue"

const artists: Artist[] = artistData
const songs: Song[] = songsData

const titleFilter = ref('')
const artistFilter = ref('')

const merged = songs.map(song=>{
  let artist = artists.find(artist=>artist._id===song.ARTIST_ID)
  return {...song,...artist}
})

const filtered = computed(() => {
  return merged.filter(song => {
    const matchesTitle = song.TITLE.toLowerCase().includes(titleFilter.value.toLowerCase())
    const matchesArtist = song.artist.toLowerCase().includes(artistFilter.value.toLowerCase())
    return matchesTitle && matchesArtist
  })
})

</script>

<template>
  <div class="container">
    <h1>Songs Selection</h1>
    <div class="filter">
      <div>
        <p>Title:</p>
        <input v-model="titleFilter" type="text">
      </div>
      <div>
        <p>Artist:</p>
        <input v-model="artistFilter" type="text">
      </div>
    </div>
    <Main :songs="filtered"></Main>  
  </div>
</template>

<style scoped>
  .filter{
    display: flex;
    flex-direction: row;
    align-items: center;
  }
</style>

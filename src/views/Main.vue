<script setup lang="ts">
import { Song } from "../models/song.ts";
import { Artist } from "../models/artist.ts";

defineProps<{songs: object}>()
</script>

<template>
    <table>
        <thead>
            <tr>
                <th>Title</th>
                <th>Artist</th>
                <th>Year</th>
                <th>Time</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="song in songs">
                <td>{{ song.TITLE }}</td>
                <td>{{ song.artist }}</td>
                <td>{{ song.YEAR }}</td>
                <td>{{ song.TIME }}</td>
            </tr>
        </tbody>
    </table>
</template>

<style>
</style>
<template>
    <div
        v-for="photo in photos"
        :key="photo.id"
    >
        <img 
            :src="photo.thumbnailUrl"
        />
        <p style="font-weight:bold">
            Name
        </p>
        
        <p>
            {{ photo.title }}
        </p>

    </div>
    
    
</template>


<script>

import { computed, watchEffect } from 'vue'
import { useStore } from 'vuex'
import { useRoute } from 'vue-router'

export default {

    setup() {
        const store = useStore()
        const route = useRoute()

        watchEffect(() => {
            const id = route.params.id
            if (!id) {
                return
            }
            store.dispatch('photos/getByAlbum', {albumId: id})
        })

        const photos = computed(() => {
            console.log(photos)
            return store.state.photos.all
        })
        return {
            photos
        }
    }
}
</script>


<style scoped>

p {
    background-color: whitesmoke;

    padding: 2px;
    
    border-style: dashed;
    border-color: black;
    border-width: 2px;
}

img {
    border-radius: 10px;
}
div {
    margin: 5px;
    margin-bottom: 10px;
    width: 150px;
    display: inline-table;
    text-align: center;
    background-color: aliceblue;
    box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;


    border-style: solid;
    border-radius: 15px;
    border-color: black;
    border-width: 2px;
}

div:hover {
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;

}
</style>
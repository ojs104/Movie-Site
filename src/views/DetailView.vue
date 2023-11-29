<template>
    <HeaderSection />
</template>


<script>
import DetailIntro from "@/components/detail/DetailIntro.vue"
import { onMounted, ref } from "vue";
import { useRoute } from 'vue-router';

export default {
    components: {
        DetailIntro
    },

    setup() {
        const movieInfo = ref([]);
        const route = useRoute();

        const movieInfoFetch = () => {
            const movieId = route.params.movieId;
            const apiKey = import.meta.env.VITE_API_KEY;
            const language = "ko-KR"
            const url = `https://api.themoviedb.org/3/${language}/movie/${movieId}?api_key=${apiKey}`

            fetch(url)
                .then((response) => response.json())
                .then((res) => {
                    console.log(res)
                    movieInfo.value = res;
                })
                .catch((error) => {
                    console.error("Error:", error)
                });
        };

        onMounted(() => {
            movieInfoFetch();
        })
    }
}
</script>
<style lang="scss">
.eader__intro {
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    position: relative;
    padding: 30px;

    &::before {}


}
</style>

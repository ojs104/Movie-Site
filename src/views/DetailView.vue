<template>
    <header id="header" role="banner">
        <div class="header__inner">
            <div class="header__bar">
                <h1>
                    <a href="/">CinemaDream</a>
                </h1>
                <nav>
                    <ul>
                        <li><a href="#">Movie top 10</a></li>
                        <li><a href="#">Drama top 10</a></li>
                    </ul>
                </nav>
            </div>

        </div>
    </header>
    <main id="main">
        <DetailIntro v-if="movieBasic" :movieBasic="movieBasic" />
        <DetailCredits v-if="movieCredits" :movieCredits="movieCredits" />
        <!-- <DetailInfo v-if="movieInfo" :movieInfo="movieInfo" />
        <DetailReview v-if="movieReview" :movieReview="movieReview" /> -->

    </main>
</template>


<script>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axios from 'axios';

import DetailIntro from "../components/detail/DetailIntro.vue"
import DetailCredits from "../components/detail/DetailCredits.vue"
// import DetailInfo from "../components/detail/DetailInfo.vue"
// import DetailReview from "../components/detail/DetailReview.vue"

export default {
    name: "MovieDetailPage",

    components: {
        DetailIntro,
        DetailCredits
        // DetailInfo,
        // DetailReview,
    },

    setup() {
        const movieBasic = ref(null);
        const movieCredits = ref([]);
        // const movieInfo = ref(null);
        // const movieReview = ref(null);

        const route = useRoute();

        onMounted(async () => {
            const movieId = route.params.movieId;
            const apiKey = import.meta.env.VITE_API_KEY;
            const language = "ko-KR";

            try {
                const resMovieBasic = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`);
                movieBasic.value = resMovieBasic.data;

                // const resMovieInfo = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`);
                // movieInfo.value = resMovieInfo.data;
                // console.log(resMovieInfo.data)

                // const resMovieReview = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`);
                // movieReview.value = resMovieReview.data;
                // console.log(resMovieReview.data)

                const resMovieCredits = await axios.get(`https://api.themoviedb.org/3/movie/${movieId}/credits?language=${language}&api_key=${apiKey}`);
                movieCredits.value = resMovieCredits.data.cast;
                console.log(resMovieCredits.data.cast)
            } catch (err) {
                console.log(err)
            }
        });

        return { movieBasic, movieCredits }
    }
}

</script>

<style lang="scss">
.detail__intro {
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    position: relative;
    padding: 30px;

    &::before {
        content: '';
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        background-color: #00000032;
        backdrop-filter: blur(7px);
        z-index: 1;
    }

    .container {
        display: flex;
        justify-content: space-between;
        position: relative;
        z-index: 10;

        .left {
            width: 350px;

        }

        .right {
            width: calc(100% - 390px);

            h2 {
                font-size: 30px;
                margin-bottom: 10px;
            }

            .desc {
                margin-bottom: 10px;
            }

            .average {
                margin-bottom: 20px;
            }

            .credits {
                display: flex;

                div {
                    width: 100px;
                    margin-right: 10px;
                }
            }
        }
    }
}
</style>
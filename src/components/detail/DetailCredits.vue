<template>
    <div class="detail__credits">
        <div class="container">
            <h3>영화 속 배우</h3>
            <div v-for="(movie, key) in movieCredits" :key="key">
                <img :src="'https://image.tmdb.org/t/p/w500' + movie.profile_path">
            </div>
            <!-- <div class="movie play__icon" v-for="movie in movies" :key="movie.id">
                <a :href="'/detail/' + movie.id">
                    <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title">
                </a>
            </div> -->
        </div>
    </div>
</template>
<script>
export default {
    props: {
        movieBasic: {
            type: Array,
            required: true,
        },
    },
    mounted() {
        console.log(this.movieBasic);
    },
}
</script>

<style lang="scss">
.detail__credits {
    h3 {
        font-size: 30px;
        margin-top: 20px;
    }
}
</style>
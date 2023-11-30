<template>
    <div class="detail__intro"
        :style="{ backgroundImage: 'url(https://image.tmdb.org/t/p/w500/' + movieBasic.background_path + ')' }">
        <div class="container">
            <div class="left play__icon">
                <a href="#">
                    <img :src="'https://image.tmdb.org/t/p/w500/' + movieBasic.poster_path" :alt="movieBasic.title">
                </a>
            </div>
            <div class="right">
                <h2>{{ movieBasic.title }}{{ movieBasic.original_title }}</h2>
                <p class="desc">{{ movieBasic.overview }}</p>
                <p>기본언어 : {{ movieBasic.original_language }}</p>
                <p>인기 : {{ movieBasic.popularity }}점</p>
                <p>개봉 날짜{{ movieBasic.release_date }}</p>
                <p>영화시간: {{ movieBasic.runtime }} 분</p>
                <div>장르 :
                    <span v-for="genre in movieBasic.genres" :key="genre.id" class="genre">
                        {{ genre.name }}
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        movieBasic: {
            type: Object,
            required: true,
        },
    }
}
</script>


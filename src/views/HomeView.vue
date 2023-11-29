<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';

const movies = ref([]);
const searchKeyword = ref(''); // 검색어를 저장할 ref를 추가

const searchMovies = async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: 'e08ff74d46031c4340e5e155300c6be8',
        language: 'ko-KR',
        page: '1',
        query: searchQuery.value,
      },
    });
    movies.value = response.data.results;
  } catch (err) {
    console.error(err);
  }
}

const fetchMovies = async (category) => {
  let url = 'https://api.themoviedb.org/3/movie/popular';
  switch (category) {
    case 'latest':
      url = 'https://api.themoviedb.org/3/movie/now_playing';
      break;

    case 'popular':
      url = 'https://api.themoviedb.org/3/movie/popular';
      break;

    case 'upcoming':
      url = 'https://api.themoviedb.org/3/movie/upcoming';
      break;

    case 'toprated':
      url = 'https://api.themoviedb.org/3/movie/toprated';
      break;
  }
  try {
    const response = await axios.get(url, {
      params: {
        api_key: 'e08ff74d46031c4340e5e155300c6be8',
        language: 'ko-KR',
        page: '1',
      },
    });
    console.log(response.data.results)
    movies.value = response.data.results;
  } catch (err) {
    console.log(err)
  }
}
</script>

<template>
  <HeaderSection />
  <main id="main" role="main">
    <div class="container">
      <div class="movie__inner">

        <section class="movie__search">
          <h2 class="blind">검색하기</h2>
          <input type="search" v-model="searchKeyword" placeholder="검색어를 입력해주세요!" @keyup.enter="serachMovies">
          <button type="submit" @click="serachMovies">검색</button>
        </section>
        <!-- //movie__search -->

        <div class="movie__tag">
          <ul>
            <li><a href="#" @click="fetchMovies('latest')">최신 영화</a></li>
            <li><a href="#" @click="fetchMovies('popular')">인기 영화</a></li>
            <li><a href="#" @click="fetchMovies('upcoming')">개봉 예정</a></li>
            <li><a href="#" @click="fetchMovies('toprated')">최고 평점</a></li>
          </ul>
        </div>
        <!-- //movie__tag -->

        <section class="movie__cont">
          <h2 class="blind">영화</h2>
          <div class="movie play__icon" v-for="movie in movies" :key="movie.id">
            <a :href="'/detail/' + movie.id">
              <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title">
            </a>
          </div>
        </section>
        <!-- //movie__cont -->

      </div>
    </div>
  </main>
  <FooterSection />
</template>

<style lang="scss">
.movie__search {
  margin: 50px 0 20px;
  position: relative;

  input {
    border: 1px solid var(--black600);
    padding: 1rem 2rem;
    width: 100%;
    border-radius: 50px;
  }

  button {
    position: absolute;
    right: 6px;
    top: 6px;
    width: 40px;
    height: 40px;
    background-color: var(--black);
    color: #fff;
    border-radius: 50%;
    cursor: pointer;
    font-size: 14px;
  }
}

.movie__tag {
  ul {
    display: flex;

    li {
      a {
        border: 1px solid var(--black);
        padding: 0.5rem 1.3rem;
        display: inline-block;
        border-radius: 50px;
        margin-bottom: 20px;
        margin-right: 10px;
        margin-top: 20px;
        font-family: "nexonLv1";


        &:hover {
          background-color: var(--black);
          color: var(--white);
        }
      }
    }
  }



}

.movie__cont {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;

  .movie {
    width: 24%;
    margin-bottom: 1.5%;
    background-color: #ccc;
  }
}
</style>

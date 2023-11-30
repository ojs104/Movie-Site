<script setup>

import { onMounted, ref } from 'vue';
import axios from 'axios';

const movies = ref([]);
const searchQuery = ref('');// 검색어를 저장할 ref를 추가

const searchMovies = async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: 'e08ff74d46031c4340e5e155300c6be8',
        language: 'ko-KR',
        query: searchQuery.value,
      }
    });
    movies.value = response.data.results;
  } catch (err) {
    console.log(err);
  }
}

const fetchMovies = async (category) => {
  let url = 'https://api.themoviedb.org/3/movie/popular'
  switch (category) {
    case 'latest':
      url = 'https://api.themoviedb.org/3/movie/now_playing'
      break;

    case 'popular':
      url = 'https://api.themoviedb.org/3/movie/popular'
      break;

    case 'toprated':
      url = 'https://api.themoviedb.org/3/movie/top_rated'
      break;
    case 'upcoming':
      url = 'https://api.themoviedb.org/3/movie/upcoming'
      break;
  }
  try {
    const response = await axios.get(url, {
      params: {
        api_key: 'e08ff74d46031c4340e5e155300c6be8',
        language: 'ko-KR',
        page: "1"
      }
    });
    console.log(response.data.results);
    movies.value = response.data.results;
  } catch (err) {
    console.log(err)
  }
}

onMounted(async () => {
  // 초기 페이지 로딩 시 최신 영화를 가져옴
  await fetchMovies('latest');
});

</script>

<template>
  <HeaderSection />
  <div class="header__intro"
    style="background-image: url(https://image.tmdb.org/t/p/w500/4fLZUr1e65hKPPVw0R3PmKFKxj1.jpg);">
    <div class="container">
      <div class="left play__icon">
        <img src="https://image.tmdb.org/t/p/w500/1YYL1OcgjPLjAGi6n0iZe1gdl9i.jpg" alt="엘리멘탈">
      </div>
      <div class="right">
        <h2>엘리멘탈</h2>
        <p class="desc">불, 물, 공기, 흙 4개의 원소들이 살고 있는 엘리멘트 시티. 재치 있고 불처럼 열정 넘치는 앰버는 어느 날 우연히 유쾌하고 감성적이며 물 흐르듯
          사는 웨이드를 만나 특별한 우정을 쌓으며, 지금껏 믿어온 모든 것들이 흔들리는 새로운 경험을 하게 되는데...</p>
        <p class="date">개봉: 2023.06.14</p>
        <p class="rating">평점: 7.727</p>
        <div class="credit">
          <p>출연진</p>
          <div>
            <img src="https://image.tmdb.org/t/p/w500/liV9OXUeo7T19hhjFlqTELtETnW.jpg" alt="actorimg"
              style="max-width: 100px;">
            <p class="actor">Leah Lewis</p>

          </div>
          <div>
            <img src="https://image.tmdb.org/t/p/w300/iPx1s7EuBEmty7MXdKSBpEBsGYT.jpg" alt="actorimg"
              style="max-width: 100px;">
            <p class="actor">Ronnie del Carmen</p>
          </div>
          <div>
            <img src="https://image.tmdb.org/t/p/w500/i9m2RGrANNxidj0bVKlSs0zHPNX.jpg" alt="actorimg"
              style="max-width: 100px;">>
            <p class="actor">Shila Ommi</p>
          </div>
          <div>
            <img src="https://image.tmdb.org/t/p/w500/d8VKC8Ms3u9XiW4e4jsy2grP02d.jpg" alt="actorimg"
              style="max-width: 100px;">>
            <p class="actor">Wendi McLendon-Covey</p>
          </div>
          <div>
            <img src="https://image.tmdb.org/t/p/w500/gI2RyymLJ9ZrhEyJSD5EqSvFpCX.jpg" alt="actorimg"
              style="max-width: 100px;">>
            <p class="actor">JCatherine O'Hara</p>
          </div>
          <div>
            <img src="https://image.tmdb.org/t/p/w500/rhXmrh7dWkCAj23MhGfI79jcbjN.jpg" alt="actorimg"
              style="max-width: 100px;">>
            <p class="actor">Mason Wertheimer</p>
          </div>
          <div>
            <img src="https://image.tmdb.org/t/p/w500/uZQu5zBGxE62uGP7qaGhjQ79bn3.jpg" alt="actorimg"
              style="max-width: 100px;">>
            <p class="actor">Ronobir Lahiri</p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <main id="main" role="main">
    <div class="container">
      <div class="movie__inner">
        <div class="movie__search">
          <h2 class="blind">검색하기</h2>
          <input tpye="search" v-model="searchQuery" type="search" placeholder="검색어를 입력해주세요!" @keyup.enter="searchMovies">
          <button type="submit" @click="searchMovies">click</button>
        </div>
        <!-- movie__search -->

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

<script>
import HeaderSection from '@/components/section/HeaderSection.vue';
import FooterSection from '@/components/section/FooterSection.vue';

export default {
  name: "MovieHomePage",
  components: {
    HeaderSection,
    FooterSection,
  },
  data() {
    return {
      movie: [],
    }
  },
  methods: {
    async search(query) {
      try {
        const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=32ba541f2b53cf63dc83a7c31682ce72&language=ko-KR&=${query}`);
        const result = await response.json();
        console.log(result);
      } catch (error) {
        console.log(error)
      }
    },
    async tags(query) {
      try {
        const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=32ba541f2b53cf63dc83a7c31682ce72&language=ko-KR&=${query}`);
        const result = await response.json();
        console.log(result);
      } catch (error) {
        console.log(error)
      }
    },
  }
}
</script>

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
    margin: 10px;
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
  }
}
</style>

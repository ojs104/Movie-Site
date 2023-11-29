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
            <div class="header__intro"
                style="background-image: url(https://image.tmdb.org/t/p/w500/4fLZUr1e65hKPPVw0R3PmKFKxj1.jpg);">
                <div class="container">
                    <div class="left">
                        <img src="https://image.tmdb.org/t/p/w500/1YYL1OcgjPLjAGi6n0iZe1gdl9i.jpg" alt="">
                    </div>
                    <div class="right">
                        <h2>엘리멘탈</h2>
                        <p class="desc">불, 물, 공기, 흙 4개의 원소들이 살고 있는 엘리멘트 시티. 재치 있고 불처럼 열정 넘치는 앰버는 어느 날 우연히 유쾌하고 감성적이며 물 흐르듯
                            사는 웨이드를 만나 특별한 우정을 쌓으며, 지금껏 믿어온 모든 것들이 흔들리는 새로운 경험을 하게 되는데...</p>
                        <p class="date">개봉: 2023.06.14</p>
                        <p class="average">평점: 7.727</p>
                        <div class="credit">
                            <ul>
                                <li>
                                    <img src="https://image.tmdb.org/t/p/w500/mT4nBq136sHYEJBjeoZzRGBIjxt.jpg"
                                        alt="Leah Lewis">
                                </li>
                                <li>
                                    <img src="https://image.tmdb.org/t/p/w500/x8tDKAgxMKwaNJSd9RB75EIJnOD.jpg"
                                        alt="Leah Lewis">
                                </li>
                                <li>
                                    <img src="https://image.tmdb.org/t/p/w500/lDYjEyqojUs2sF3CgdsOZ9vr2KL.jpg"
                                        alt="Leah Lewis">
                                </li>
                                <li>
                                    <img src="https://image.tmdb.org/t/p/w500/51v6jsvzuAXYirIzdqcjLBp46d6.jpg"
                                        alt="Leah Lewis">
                                </li>
                                <li>
                                    <img src="https://image.tmdb.org/t/p/w500/lDYjEyqojUs2sF3CgdsOZ9vr2KL.jpg"
                                        alt="Leah Lewis">
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

<style lang="scss">
.header__inner {
    .header__bar {
        display: flex;
        justify-content: space-between;
        width: 100%;
        height: 60px;
        background: #222;

        h1 {
            padding: 15px 25px;
            font-size: 22px;
            text-align: center;
            color: var(--white);
        }

        nav {

            ul {
                display: flex;
                justify-content: space-between;
                padding: 20px 25px;

                li {
                    display: inline;

                    a {
                        display: inline-block;
                        color: var(--white);
                        padding: 0 10px;
                    }
                }
            }
        }
    }

    .header__intro {
        padding: 30px;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center;
        position: relative;

        &::before {
            position: absolute;
            content: '';
            width: 100%;
            height: 100%;
            left: 0;
            top: 0;
            background-color: #dadada36;
            backdrop-filter: blur(7px);
            z-index: 1;
        }

        .container {
            position: relative;
            justify-content: space-between;
            display: flex;
            z-index: 10;

            .left {
                width: 350px;

                img {
                    width: 100%;
                    vertical-align: top;
                }
            }

            .right {
                width: calc(100% - 390px);
                background-color: #ffffff1a;

                h2 {
                    font-size: 30px;
                    margin-bottom: 10px;
                }

                .desc {
                    margin-bottom: 10px;
                }

                .date {
                    display: inline-block;
                    margin-right: 20px;
                }

                .average {
                    display: inline-block;
                    margin-bottom: 30px;
                }

                .credit {
                    display: flex;

                    li {
                        width: 50px;

                        img {
                            width: 100%;
                        }
                    }
                }
            }
        }
    }
}
</style>
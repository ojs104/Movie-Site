<template>
    <footer id="footer" role="contentinfo">
        <div class="container">
            <div class="footer__top">
                <div class="footer__title">Cinema<br /><em>Dream</em></div>
                <nav class="footer__nav">
                    <ul>
                        <li><a href="#">Home</a></li>                        
                        <li><a href="#">Movies</a></li>                     
                    </ul>
                </nav>
            </div>
            <div class="footer__bottom">
                <div class="footer__email">
                    kmdojs@gmail.com
                </div>
                <div class="footer__copy">
                    <p>&copy; 2023 J.S. All rights reserved.</p>
                </div>
            </div>
        </div>
    </footer>
</template>

<style lang="scss">
#footer {
    background-color: var(--black);

    .footer__top {
        display: flex;
        align-items: center;
        justify-content: flex-start;
        width: 100%;
        min-height: 200px;

        .footer__title {
            text-align: center;
            font-family: var(--Title-font);
            line-height: 0.6;
            font-size: 3rem;
            color: white;

            em {
                font-size: 2.5rem;
                color: var(--white);
                letter-spacing: 5px;
            }
        }

        .footer__nav {
            width: 100%;

            ul {
                display: flex;
                justify-content: flex-end;


                li {
                    display: inline-block;
                }

                a {
                    font-size: 1rem;
                    font-weight: 300;
                    color: var(--white );
                    padding: 15px 30px;
                    transition: all 0.3s;
                    text-decoration: underline;
                    text-underline-position: under;
                }
            }
        }
    }

    .footer__bottom {
        font-size: 1rem;
        text-align: center;
        margin-bottom: 10px;

        .footer__email {
            color: var(--white);
        }

        .footer__copy {
            p {
                color: var(--white);
            }
        }
    }
}
</style>
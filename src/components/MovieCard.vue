<template>
    <div class="modal_background" 
    @click="hideModal(movie)" >
        <div class="modal_outer">
                <button class="close" @click="hideModal(movie)" >
                    X
                    <div class="btn_inner"></div> 
                </button>
                <img class="modal_img" :src="movie.posterUrl" alt="">
                <div class="modal_text">
                    <h2>{{movie.nameRu}}</h2>

                    <span class="fa fa-star "></span>
                    <span class="fa fa-star "></span>
                    <span class="fa fa-star "></span>
                    <span class="fa fa-star"></span>
                    <span class="fa fa-star"></span>

                    <div class="star_wrapper" :style="{ width: (+movie.rating/10)*65 + 'px' }">
                        <span class="fa fa-star checked"></span>
                        <span class="fa fa-star checked"></span>
                        <span class="fa fa-star checked"></span>
                        <span class="fa fa-star checked"></span>
                        <span class="fa fa-star checked"></span>
                    </div>
                     
               <br> <span>Год:</span> {{movie.year}}
               <br> <span>Страны:</span> <span class="normal" v-for="country, i in movie.countries">{{i == movie.countries.length - 1 ? country.country : country.country + ', '}} <span class="hidden">_</span> </span>
               <br><span>Рейтинг:</span> {{movie.rating}}
               <br> <span>Жанры:</span>  <span class="normal" v-for="genre, i in movie.genres">{{i == movie.genres.length - 1 ? genre.genre : genre.genre + ', '}} <span class="hidden">_</span>  </span>
               <br> <span>Длительность:</span> {{movie.filmLength}}
                </div>
        </div>
    </div>
</template>

<script>
    export default {
        
        name: 'MovieCard',
        props: ['movie', 'hideModal', 'pageYOffset'],
        
    }
</script>

<style scoped>
    .modal_background {
        width: 180vh;
        height: 320vh;
        background: rgba(0, 0, 0, 0.6);
        display: flex;
        justify-content: center;
        align-items: start;
        padding-top: 50px;
        position: absolute;
    }

    .modal_outer {
        width: 110vh;
        height: 80vh;
        margin-top: 120px;
        margin-left: -90px;
        /* background: #1a191f; */
        background: #000;
        /* background-image: url(../assets/mortalCombat.jpeg); */
        background-size: cover;
        background-repeat: no-repeat;
        background-position: top;
        box-shadow: 0px 0px 10px 10px rgba(0, 0, 0, 0.677);
        padding: 30px;
        display: flex;
        justify-content: space-between;
        position: fixed;
    }

    .modal_img {
        position: absolute;
        max-height: 70vh;
        border-radius: 5px;
        box-shadow: 0px 0px 50px 15px rgb(49 49 49 / 41%);
    }

    .modal_text {
        width: 50vh;
        height: 70vh;
        color: aliceblue;
        text-align: justify;
    }

    h2 {
        font-size: 35px;
        margin-top: 70px;
        margin-bottom: 0px;
    }

    span {
        font-size: 14px;
        color: #ffd80e;
        display: inline-flex;
    }

    .normal {
        color: aliceblue;
        font-size: 16px;
    }

    .close {
        width: 70px;
        height: 50px;
        font-weight: 100;
        font-size: 30px;
        position: relative;
        left: 90%;
        top: 2%;
        background: transparent;
        border: 1px solid aliceblue;
        border-radius: 2px;
        color: aliceblue;
        opacity: 0.6;
    }
    .btn_inner {
        width: 64px;
        height: 44px;
        position: absolute;
        top: 2px;
        left: 2px;
        border: 1px solid aliceblue;
        border-radius: 1px;
    }
    .fa-star {
        color: rgb(179, 175, 175);
    }
    .checked {
        color: orange;
    }

    .star_wrapper {
        width: 65px;
        max-height: 25px;
        /* border: 1px solid white; */
        overflow: hidden;
        position: relative;
        /* top: 402px; */
        left: -65px;
        /* left: 653px;
        left: 70.2%; */
        display: inline-flex;
    }
    .info {
        color: aliceblue;
    }

    .hidden {
        color: transparent;
    }
</style>
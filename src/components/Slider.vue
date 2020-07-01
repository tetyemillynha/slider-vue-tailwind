<template>
  <div class="container mx-auto py-4">
    <h1 class="title-xl text-gray-800 text-center">{{msg}}</h1>
    <div class="box-content w-100 p-4">
        <transition name="fade" mode="out-in">
            <div v-for="index in [currentIndex]" :key="index">
                <img class="h-auto mx-auto" :src="currentImg"/>
            </div>
        </transition>

        <div class="slider-controls inline-flex py-4">
            <button class="btn-gray btn-prev" @click="plusSlides(-1)" type="button">Anterior</button>
            <button class="btn-gray btn-next" @click="plusSlides(1)" type="button">Próximo</button>
        </div>

        <div class="grid grid-flow-col grid-rows-3 sm:grid-rows-3 md:grid-rows-2 lg:grid-rows-1 xl:grid-rows-1">
            <div v-for="(item, key, index) in images" :key="index" class="text-gray-700 text-center m-2">
                <img @click="currentSlide(key)" class="w-full rounded shadow-lg" :src="item"/>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Slider',
    props: {
        msg: String
    },
    data(){
        return{
        images: [
            'https://cdn.pixabay.com/photo/2020/04/13/17/16/netherlands-5039354_960_720.jpg', 
            'https://cdn.pixabay.com/photo/2016/11/08/05/11/children-1807511_960_720.jpg', 
            'https://cdn.pixabay.com/photo/2020/04/09/11/42/dogs-5021084_960_720.jpg', 
            'https://cdn.pixabay.com/photo/2014/04/13/20/49/cat-323262_960_720.jpg', 
            'https://cdn.pixabay.com/photo/2013/07/18/20/26/boat-164989_960_720.jpg'
        ],
        currentIndex: 0,
        timer: null
        }
    },

    //Function call that automatically rotates the slides every 5 seconds
    mounted: function(){
        this.startSlide();
    },

    //Methods(functions)
    methods:{
        //rotate slides every 8 seconds  
        startSlide: function(){
            const self = this;
            this.timer = setInterval(function(){
                self.currentIndex++;
            }, 5000);
        },
        //prev and next buttons
        plusSlides: function(n){
            this.currentIndex += n;
            clearInterval(this.timer);
        },
        //current clicked image
        currentSlide: function (n){
            this.currentIndex = n;
            clearInterval(this.timer);
        }
    },

    //Image URL
    computed: {
        currentImg: function(){
            return this.images[Math.abs(this.currentIndex) % this.images.length];
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .fade-enter-active, .fade-leave-active {
        transition: opacity .4s;
    }
     /* .fade-leave-active below version 2.1.8 */
    .fade-enter, .fade-leave-to{
        opacity: 0;
    }
    .img-slider {
        height:640px;
    }
</style>

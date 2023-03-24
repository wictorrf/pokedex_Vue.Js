<template>
    <div class="column">
        <div class="card column has-background-dark">
        <div class="card-image">
            <figure>
            <img :src="currentImg" alt="Placeholder image" width="150">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4 has-text-warning">{{num}} - {{upper}}</p>
                <p class="subtitle is-6 has-text-warning">{{pokemon.type}}</p>
            </div>
            </div>

            <div class="content">
                <button class="button is-medium is-fullwidth" @click="mudarSprit">Mudar Sprit</button>
            </div>
        </div>
        </div>
    </div>
</template>
<script>
import axios from "axios";

export default {
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
            console.log(this.pokemon)
        })
    },
    data(){
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    computed: {
        upper: function() {
         return this.name.charAt(0).toUpperCase() + this.name.slice(1);
        },
    },
    methods: {
        mudarSprit: function(){
            if (this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            } else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>
<style >
.card{
    margin-top: 20px;
}
</style>
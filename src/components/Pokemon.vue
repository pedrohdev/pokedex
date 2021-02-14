<template>
    <div @mouseup="change" class="column is-half is-offset-one-quarter" align="center">
        <div class="card">
            <div class="card-image">
                <figure>
                    <img :src="pokemon.image" :alt="nome">
                </figure>
            </div>
            <div class="card-content">

                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{ num }} - {{ nome | upper}}</p>
                        <p class="subtitle is-6">{{ pokemon.type }}</p>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "Pokemon",
    props: {
        nome: String,
        url: String,
        num: Number
    },
    filters: {
        upper(value){
            return value[0].toUpperCase() + value.slice(1)
        }
    },
    data(){
        return {
            pokemon: {
                type: '',
                front: '',
                back: '',
                image: ''
            }
        }
    },
    methods: {
        change(){

            if(this.pokemon.image == this.pokemon.back){
                this.pokemon.image = this.pokemon.front
            }else{
                this.pokemon.image = this.pokemon.back
            }


            
        }
    },
    created(){
        axios.get(this.url).then((data) => {

            this.pokemon.type = data.data.types[0].type.name
            this.pokemon.front = data.data.sprites.front_default
            this.pokemon.back = data.data.sprites.back_default
            this.pokemon.image = this.pokemon.front

        }).catch((err) => {
            console.log(err)
        })
    }
}
</script>

<style>

</style>
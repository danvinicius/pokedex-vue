<template>
    <div class="card">
        <h2>{{pokemon.name}}</h2>
        <img :src="pokemon.currentImg" :alt="pokemon.name" :title="pokemon.name" @click="changeImg">
        <h5>{{pokemon.id}}</h5>
        <div class="typesContainer">
                <div v-for="type in pokemon.types" :key="type.type.name" :class="type.type.name">{{type.type.name}}</div>
        </div>
</div>
</template>

<script>
export default {
    name: 'PokemonCard',
    props: {
        name: String,
        url: String
    },
    data(){
        return {
            pokemon: {
                name: '',
                id: 0,
                currentImg: '',
                types: [],
            },
            isFront: true,
            front: '',
            back: ''
        }
    },
    created(){
        this.fetchPokemon()
    },
    methods: {
        async fetchPokemon(){
            const buscaPokemon = await fetch(this.url)
            const data = await buscaPokemon.json()
            this.setPokemonData(data)

        },
        setPokemonData(data){
            const noCapitalizedName = data.name
            const capitalizedName = noCapitalizedName[0].toUpperCase() + noCapitalizedName.slice(1)
            this.pokemon.name = capitalizedName
            this.pokemon.id = data.id
            this.front = data.sprites.front_default
            this.back = data.sprites.back_default
            this.pokemon.currentImg = this.front
            this.pokemon.types = data.types
        },
        changeImg(){
            this.isFront = !this.isFront
            this.pokemon.currentImg = this.isFront ? this.front : this.back
        }
    }
}
</script>

<style scoped>
.card {
  background-image: linear-gradient(
    to right bottom,
    #c1e1ed,
    #cfffd0
  );
  height: 300px;
  border-radius: 20px;
  padding: 20px 10px;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  position: relative;
  transition: .3s;
}
.card:hover {
    transform: scale(1.05);
}
.card h2 {
  font-size: 18px;
}
.card img {
  height: 150px;
  position: relative;
  cursor: pointer;
}
.card::before {
    content: '';
    background: #fff;
    border-radius: 50%;
    position: absolute;
    display: block;
    height: 100px;
    width: 100px;
    top: 25%;
    left: 50%;
    transform: translateX(-50%);
}
.card div {
  display: inline-block;
  border-radius: 15px;
  color: #fff;
  text-transform: uppercase;
  padding: 5px;
  display: flex;
  flex-wrap: wrap;
  font-size: 15px;
  gap: 3px;
  align-items: center;
  justify-content: center;
}
.card .normal {
  background: rgb(204, 204, 181);
}
.card .fighting {
  background: tomato;
}
.card .flying {
  background: linear-gradient(to bottom, lightblue 50%, rgb(204, 204, 181));
}
.card .poison {
  background: linear-gradient(to bottom, pink 50%, purple 50%);
}
.card .ground {
  background: linear-gradient(to bottom, gold 50%, rgb(202, 172, 0));
}
.card .rock {
  background: rgb(202, 172, 0);
}
.card .bug {
  background: gold;
}
.card .ghost {
  background: purple;
}
.card .steel {
  background: linear-gradient(
    to bottom,
    rgb(204, 204, 181) 50%,
    rgb(31, 102, 73)
  );
}
.card .fairy {
  background: linear-gradient(to bottom, lightblue 50%, pink);
}
.card .fire {
  background: orangered;
}
.card .water {
  background: rgb(58, 143, 255);
}
.card .grass {
  background: lightgreen;
}
.card .electric {
  background: orange;
}
.card .psychic {
  background: pink;
}
.card .ice {
  background: lightblue;
}
.card .dragon {
  background: linear-gradient(to bottom, rgb(58, 143, 255) 50%, tomato);
}
.card .dark {
  background: rgb(31, 102, 73);
}
</style>
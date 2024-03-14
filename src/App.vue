<template>
  <div class="contenedorPrincipal">

<div >
  <q-layout view="hHh lpR fFf">

    <q-header elevated class="bg-brown-8 text-WHITE">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://user-images.githubusercontent.com/9741252/81717987-83b84000-947b-11ea-9ac9-5ad1d59adf7a.png">
          </q-avatar>
          POKEMONN!!!
        </q-toolbar-title>
      </q-toolbar>
    </q-header>
  
    <q-page-container>
      <router-view />
    </q-page-container>



<div class="buscador">
  <input type="text" placeholder="Busca por numero" id="buscadorinput" v-model.trim="buscador">
<button id="boton" @click="traer()"><img id="logito" src="https://codeboost.com.br/projetos/pokeapi/img/img-pokeball-02.png"></button>
  </div>
  
    <div class="card">
      
      <div  class="boletacomprada">
          <div class="texto-nombrep">{{ pokemon.name }}</div>
        <div class="datop">
          <div class="texto-nombre">Peso</div>
          <div class="texto-telefono">{{ pokemon.weight }}</div>
        </div>
      <img :src="pokemon.sprites.front_shiny" alt="" v-if="pokemon.sprites">
      <img :src="pokemon.sprites.other.showdown.front_shiny" alt="" v-if="pokemon.sprites">
      <img :src="pokemon.sprites.other.showdown.back_shiny" alt="" v-if="pokemon.sprites">
        <h4 v-for="(e, i) in pokemon.types" :key="i">Tipo: {{ e.type.name }} </h4>
      </div>

      <section class="linear-progress-section">
        <div class="linear-progress" v-for="(e, i) in pokemon.stats" :key="i">
          <label :for="'ID' + i" class="stat-name text-xs font-semibold text-black">{{ e.stat.name }}</label>
          <q-linear-progress :id="'ID' + i" :value="progressValue(e.base_stat)" :buffer="bufferValue(e.base_stat + 10)" rounded size="10px" color="blue">
            <div class="absolute-full flex flex-center">
              <q-badge color="white" text-color="accent" :label="e.base_stat" />
            </div>
          </q-linear-progress>
        </div>
      </section>

  </div>

    <q-footer class="bg-brown-5 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://codeboost.com.br/projetos/pokeapi/img/img-pokeball-02.png">
          </q-avatar>
          <div>POKEDEX!!!</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

  </q-layout>
</div>
  </div>
</template>

<script setup>
import {ref} from "vue"
import axios from "axios"

let pokemon = ref([])
let buscador = ref([])



async function traer() {
  try {
    let r = await axios.get("https://pokeapi.co/api/v2/pokemon/"+buscador.value)
    pokemon.value=r.data
    console.log(r.data);
  } catch (error) {
    console.log(error);
  } 
}
const progressValue=(baseStat)=>`0.${baseStat}`
const bufferValue=(baseStat)=>`0.${baseStat+10}`

</script>

<style>


.card{
  width: 70vw;
  height: 60vh;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid rgb(255, 255, 255); 
}
.buscador {
  margin-left: 20%;
  width: 17vw;
  height:7vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: cadetblue;
  box-shadow: 4px 8px 16px rgba(0, 0, 0, 0.5);
  margin-top:-20%

}

#logito{
  width:2vmax;
  height:3vmax;
  cursor: pointer;
  box-sizing: border-box;
  padding: 78%;

}


#boton{
  width:2vmax;
  height:2vmax;
  display:flex;
  justify-content: center;
  align-items: center;
  background-color: cadetblue;
}

#buscadorinput{
  width:85%;
  height:90%;
  background-color: cadetblue;
  color:black;
  border: 3px solid cadetblue;
  box-sizing: border-box;
  padding-left: 3%;

}
</style>

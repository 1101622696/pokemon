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
  <input type="text" placeholder="Busca un pokemon" id="buscadorinput" v-model.trim="buscador">
<button id="boton" @click="traer()"><img id="logito" src="https://codeboost.com.br/projetos/pokeapi/img/img-pokeball-02.png"></button>
  </div>
  
    <div class="card">
        <div class="imagenes">
          <div class="imgprincipal">
      <img id="imgprincipal" :src="pokemon.sprites.front_shiny" alt="" v-if="pokemon.sprites">
    </div>
      <img id="imgdetras" :src="pokemon.sprites.other.showdown.front_shiny" alt="" v-if="pokemon.sprites">
      <img id="imgdetras" :src="pokemon.sprites.other.showdown.back_shiny" alt="" v-if="pokemon.sprites">
    </div>
    <div  class="datos" v-if="showcard">
      <div class="nombre">{{ pokemon.name }}</div>
      <div class="tipo" v-for="(e, i) in pokemon.types" :key="i">Tipo: {{ e.type.name }} </div>
          <div class="peso">Peso: {{ pokemon.weight }}</div>
        </div>
      <section class="linear-progress-section">
        <div class="linear-progress" v-for="(e, i) in pokemon.stats" :key="i">
          <label :for="'ID' + i" rounded size="13px" color="purple" class="stat-name text-xs font-semibold text-white" >{{ e.stat.name }}</label>
          <q-linear-progress :id="'ID' + i" :value="progressValue(e.base_stat)" :buffer="bufferValue(e.base_stat + 10)" rounded size="15px" color="purple">
            <div class="absolute-full flex flex-center">
              <q-badge color="black" text-color="white" :label="e.base_stat" />
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
let showcard = ref(false);



async function traer() {
  try {
    let r = await axios.get("https://pokeapi.co/api/v2/pokemon/"+buscador.value)
    pokemon.value=r.data
    console.log(r.data);
  } catch (error) {
    console.log(error);
  } 
  showcard.value=true

}
const progressValue=(baseStat)=>`0.${baseStat}`
const bufferValue=(baseStat)=>`0.${baseStat+10}`

</script>

<style>


.card{
  width: 80vw;
  height: 60vh;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-sizing: border-box;
}
.buscador {
  margin-left: 20%;
  width: 17vw;
  height:8vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: cadetblue;
  box-shadow: 4px 8px 16px rgba(0, 0, 0, 0.5);
  margin-top:-30%

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
#boton:hover{
  border:none;
  outline:none
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

.datos{
  width:50vh;
  height:30vh;
  display:flex;
  box-sizing: border-box;
  flex-direction: column;
  justify-content: space-between;
  color:white;
  }
.tipo{
  font-size: 20px;

}
.nombre{
color:purple;
font-weight: 700;
font-size:50px;
backdrop-filter: blur(55px);
text-transform:uppercase;
font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}
.peso{
text-decoration: underline;
font-size: 15px;
}
.imagenes{
  width:50vh;
  height:100%;
}
section{
  width:60vh;
  height:100%;
  box-sizing: border-box;
  top: 5%;
  color:white
}
.imgprincipal{
  width:100%;
  height:60%;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
}
#imgprincipal{
  margin-top: -22%;
  aspect-ratio: 16/9;
  width:400px;
  height:250px;
  filter: drop-shadow(
    0 0 10px rgb(0, 0, 0, .8)
  )
}

#imgdetras{
  width:40%;
  height:30%;
}
.linear-progress{
padding: 2%;
}

</style>


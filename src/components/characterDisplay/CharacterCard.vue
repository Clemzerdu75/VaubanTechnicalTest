<template>
  <div class="Card"
      :style=" character.selected ? 'background-color: #bdbdbd' : 'background-color: white' ">

    <div class="topRow">
        <h1 style="font-size: 2.5em" >{{character.name}}</h1>
        <h3 v-on:click="character.selected = !character.selected"> {{ character.selected ? "-" : "+"}}</h3>
    </div>

    <div class="middleRow">
      <h2>{{character.height}}cm</h2>
      <h2>{{character.mass}}kg </h2>
    </div>

    <div class="middleRow infosWrapper">
      <div >
        <h2 class="infos"><strong>Birth Year:</strong>&nbsp;{{character.birth_year}}</h2>
        <h2 class="infos"><strong>Hair:</strong>&nbsp;{{character.gender === "n/a" ? "Robot" : character.hair_color}}</h2>
      </div>
      <div style="text-align: right; width: 40%">
        <h2 class="infos"><strong>Skin:</strong>&nbsp;{{character.skin_color}}</h2>
      </div>
    </div>

    <div class="middleRow" style="font-size: 1.5em; justify-content: space-around;" >
      <h2 v-on:click="character.selected ? () => null : handleExpand(1) " :style="species.status ? 'color:black' : 'color:grey'">Specie</h2>
      <h2 v-if="starships.data.length" v-on:click="character.selected ? () => null : handleExpand(2) " :style="starships.status ? 'color:black' : 'color:grey'">Starships</h2>
    </div>

    <div v-if="species.status" class="moreInfos" style="height: 100px;">
      <p class="speciesName">{{species.data.name}}</p>
      <p style="color: grey"><strong style="color: black;">Classification:</strong> {{species.data.classification}}</p>
      <p style="color: grey; padding-bottom: 10px;"><strong style="color: black;">Designation:</strong> {{species.data.designation}}</p>
    </div>

    <div v-else-if="starships.status " class="moreInfos starshipWrapper">
      <div v-for="starship in starships.data" :key="starship.name">
        <p style="color: black; font-weight: bold">{{starship.name}}</p>
      </div>
    </div>

    <div v-else></div>

    <div class="genderWrapper"
      :style="species.status || (starships.status) ? 'opacity: 0' : 'opacity: 1'">
      <h2 class="gender" 
      :style=" character.gender === 'n/a' || character.selected  ?  
        'color: grey;' : character.gender === 'female' ? 'color: #F58C8C; ' : 'color: #7BBCDE;'">
      {{ character.gender === "n/a" ? "Robot" : character.gender === "female" ? "F" : "M" }}</h2>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {

    mounted() {
      const speciesRequest = this.character.species[0]
      const starshipRequest = this.character.starships

      axios.get(speciesRequest)
        .then((res) => this.species.data = res.data)

      const starshipArr = starshipRequest.map(l => fetch(l).then(res => res.json()));
      Promise.all(starshipArr).then(res => res ? this.starships.data = res : null)
    },

    name: 'CharacterCard',
    props:['character'],
    data () {
      return {
        species: {
          data: {},
          status: false,
        },
        starships: {
          data: [],
          status: false,
        }
      }
    },
    methods: {
      handleExpand(index) {
        if (index === 1) {
          this.species.status = !this.species.status
          this.starships.status = false
        }
        else {
          this.starships.status = !this.starships.status
          this.species.status = false
        }
      }
    }
  }

</script>

<style scoped>

  h1, h2, h3 {
      color: #0f0f0f;
  }
  .Card {
      margin: 20px;
      background-color: white;
      border-radius: 10px;
      box-shadow: 0px 2px 10px rgba(0,0,0, .6);
      width: 400px;
      height: 400px;
      transition: .2s ease-out;
      text-align: left;
      padding: 0px 15px;
      
  }
  .Card:hover {
      transform: scale(1.1);
  }

  .Card h2 {
    margin-bottom: -5px;
    font-weight: 400;
  }

  .Card h1 {
    margin-top: 10px;
  }

  .topRow {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      width: 100%;
      height: 4em;
      overflow: hidden;
  }

  .topRow h3 {
      font-size: 5em;
      text-align: left;
      transition: .2s ease-out;
      font-weight: bold;
      margin-top: -10px;
  }

  .middleRow {
    display: flex;
    flex-direction: row;
  }

  .middleRow h2{
    font-size: 1.2em;
    font-weight: 600;
    margin-top: -5px;
    margin-right: 10px;
  }

  .infos {
    font-weight: 400 !important;
    font-size: 1.5em !important;
    margin-bottom: 20px !important;
  }

  .gender {
    transition: .4s ease-out;
    font-size: 4em !important;
    text-align: right;
    padding-top: 20px;
    font-weight: 700 !important;
    color: grey;
  }

  .moreInfos {
    width: 70%;
    margin: 0 auto;
    text-align: center;
    padding: 0px 10px;
    animation-name: enter;
    animation-duration: .4s;
  }

  @keyframes enter {
      0% {opacity: 0}
      100% {opacity: 1}
  }

  h2 strong {
    color: rgb(58, 58, 58);
  }

  .infosWrapper {
    margin-top: 60px;
    justify-content: space-between;
    height: 100px;
    width: 100%;
  }

  .speciesName {
    color: black;
    text-transform: uppercase;
    font-weight: bold;
    font-size: 1.4em; margin-bottom: -5px;
    padding-top: 10px;
    letter-spacing: 3px;
  }

  .starshipWrapper {
    height: 100px;
    overflow-y: scroll;
    margin-top: 20px;
  }

</style>

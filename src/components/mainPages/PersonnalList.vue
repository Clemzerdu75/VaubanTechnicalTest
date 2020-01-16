<template>
  <div>
    <div v-on:click="handleExpand()" v-if="!expand" class="personnalList">
      <div class="topRow">
        <h3  style="color: #0f0f0f">PERSONNAL LIST</h3>
        <img  alt="expand" :src="require('./../../assets/Expand.png')"/>
      </div>
      <div class="persoList">
        <div v-for="character in characters" :key="character.name">
          <div  v-if="character.selected" class="charMiniat">
            <h3>{{character.name}}</h3>
          </div>
        </div>
      </div>
    </div>
  <div v-else class="persoListExpanded">
    
    <div class="topRow">
        <h1 style="margin-left: 20px">Personnal List</h1>
        <img class="reduce" v-on:click="handleExpand()" alt="expand" :src="require('./../../assets/Reduce.png')"/>
      </div>
      
    <div class="persoList" style="opacity: 1">
      <div v-for="character in characters" :key="character.name">
        <CharacterMiniat v-if="character.selected" :character="character" />
      </div>
    </div>
  </div>

  </div>
</template>

<script>
import CharacterMiniat from './../characterDisplay/CharacterMiniat';

export default {
  name: 'PersonnalList',
  props: ['characters', 'expand'],
  components: {
    CharacterMiniat,
  },

  methods: {
    handleExpand() {
      this.$emit('handleExpand', '');
    }
  }
}
</script>

<style scoped>

  .persoList {
    margin: 20px;
    margin-top: -40px;
    height: calc(100% - 8em);
    overflow-y: scroll;
    text-align: center;
    opacity: 0;
    transition: .8s ease-out;
  }

  .topRow {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    height: 4em;
    overflow: hidden;
    margin-bottom: 40px;
    margin-left: 10px;
  }

  .personnalList {
      filter: invert();
      background-color: #f0f0f0;
      position: fixed;
      bottom: -5px;
      right: 10px;
      width: 300px;
      height: 50px;
      transition: .4s ease-out;
      border-radius: 5px;
      border: solid 2px  black;
  }

  .personnalList h3 {
      font-size: 1.5em;
      margin: 10px 5px;
  }

  .personnalList:hover {
      height: 500px;
  }

  .personnalList:hover .persoList {
      opacity: 1;
  }

  .personnalList img {
    opacity: 0;
    width: 30px;
    height: 30px;
    transition: .2s ease-out;
    padding: 10px 10px;
  }

  .personnalList:hover img {
    opacity: 1;
    
  }

  .persoListExpanded {
    position: fixed;
    width: 30%;
    text-transform: uppercase;
    animation-name: Appear;
    animation-duration: .4s;
    border-left: solid 1px white;
    height: 100%;
    
  }

  .reduce {
    width: 40px;
    height: 40px;
    margin: 10px 10px;
  }

  .charMiniat {
    margin: 10px 10px;
    border: solid 1px black;
    color: #0f0f0f;
  }


  @keyframes Appear {
    0% {
      margin-left: 50%;
      opacity: 0
      }
    100% {
      margin-left: 0;
      opacity : 1
      }
  }

</style>

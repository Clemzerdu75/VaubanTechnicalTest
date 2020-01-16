<template>
  <div class="Card" v-on:click="character.selected = !character.selected">
        <h1>{{character.name}}</h1>
  </div>
</template>

<script>

export default {
  name: 'CharacterMiniat',
  props:['character'],
}
</script>

<style scoped>

  h1 {
      color: #f0f0f0;
      font-size: 1.5em;
      margin-top: 20px;
  }
  .Card {
      margin: 0 auto;
      border: solid 1px white;
      background-color: "transparent";
      width: 80%;
      height: 70px;
      transition: .2s ease-out;
      text-align: left;
      padding: 0px 15px;
      margin-top: 20px;
      
  }

  .Card:hover {
    background-color: white;
  }

  .Card:hover h1 {
    color: #0f0f0f;
  }
  
</style>

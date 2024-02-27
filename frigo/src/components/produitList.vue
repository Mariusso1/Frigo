<script setup>

import {ref, watch} from "vue";

const nomProduit=ref('');
const emit=defineEmits(['updateR']);

function searchProduit(nomProduit){
  emit('updateR',nomProduit)
}


watch(nomProduit, (newValue) => {
  searchProduit(newValue)
});

</script>

<template>

  <div id="rech">
    <form @submit.prevent="$emit('updateR', nomProduit)">
      <input class="sea_bar" type="text" v-model="nomProduit" placeholder="Que souhaites tu ?" required/>
      <br><br>
      <input class="sea_btn" type="submit" value=" Rechercher " />
      <br><br>
    </form>
  </div>


</template>

<style scoped>
#rech {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.sea_bar {
  width: 300px;
  height: 40px;
  border: 2px solid #4CAF50;
  border-radius: 20px;
  padding: 10px;
  font-size: 16px;
  outline: none;
  background-color: rgba(255, 255, 255, 0.8)
}

.sea_btn {
  width: 200px;
  height: 50px;
  background-color: #4CAF50;
  border: none;
  color: white;
  font-size: 20px;
  cursor: pointer;
  border-radius: 25px;
}

.sea_btn:hover {
  background-color: #45a049;
}

</style>

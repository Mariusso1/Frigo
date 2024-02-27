<script setup>

import TempForm from "@/components/TempForm.vue";

const url="https://webmmi.iut-tlse3.fr/~pecatte/frigo/public/17/produits"

function addProduit(name,quantity,picture) {
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  const fetchOptions = {
    method: "POST",
    headers: myHeaders,
    body: JSON.stringify({id: 23, nom: name, qte: quantity, photo: picture}),
  };
  fetch(url, fetchOptions)
    .then((response)=>{
      return response.json();
    })
    .then((dataJSON)=>{
      console.log(dataJSON);

    })
    .catch((error)=> console.log(error));
}


</script>

<template>

  <TempForm @addProduit="addProduit"/>

</template>

<style scoped>

</style>

<script setup>


import ProduitAjout from "@/components/produitAjout.vue";

</script>

<template>
  <v-container class="ajout">
    <v-container class="title"> Tu veux ajouter quelque chose? </v-container>
    <br><br><br><br><br><br>

    <produit-ajout />

  </v-container>

</template>

<style scoped>
.ajout {
  padding: 40px;
  min-height: 600px;
  background-image: url("imgmarché.jpg");
  background-size: cover;
  background-position: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.title {
  background-color: rgba(255, 255, 255, 0.8);
  padding: 20px 40px;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title {
  font-family: "Roboto", sans-serif;
  font-size: 48px;
  color: #2d6baf; /* Couleur du titre */
  font-weight: bold;
  text-align: center;
}




</style>

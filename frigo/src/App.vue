<template>
  <v-app>

    <header class="custom-header">
      <div class="custom-header-nav">
        <router-link to="/" class="menu-btn">Accueil</router-link>
        <div class="custom-header-title">LE FRIGO DE MARIUS</div>
        <router-link to="/PageProduits" class="menu-btn">Ajouter un Produit</router-link>
      </div>
    </header>

    <v-main>
      <v-container class="page">
        <RouterView />
      </v-container>
    </v-main>

  </v-app>
</template>

<script setup>
import { ref } from 'vue'
const drawer = ref(false)

</script>
<style scoped>
.page{
  min-height: 100vh;
  text-align: center;
}

.custom-header {
  background-color: #1976D2;
  color: white;
  padding: 10px 20px;
}

.custom-header-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.custom-header-title {
  font-size: 24px;
  font-weight: bold;
}

.menu-btn {
  color: white;
  font-weight: bold;
  text-transform: uppercase;
  text-decoration: none;
}

.menu-btn:hover {
  text-decoration: underline;
}
</style>

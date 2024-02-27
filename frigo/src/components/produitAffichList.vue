<script setup>

import {onMounted, reactive, watch} from "vue";
import Produit from "@/js/Produit"

import ProduitList from "@/components/produitList.vue";


const url = "https://webmmi.iut-tlse3.fr/~pecatte/frigo/public/17/produits";
const listeProduit = reactive([]);

let nomProduit = '';

function affichProduit() {
  fetch(url + `?search=` + nomProduit)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      listeProduit.splice(0, listeProduit.length)
      for (let produit of dataJSON) {
        listeProduit.push(new Produit(produit.id, produit.nom, produit.qte, produit.photo))
      }
    })
    .catch((error) => {
      console.log(error);
    });
}

onMounted(() => {
  affichProduit();
})

function updateR(name) {
  nomProduit = name
  affichProduit()
}

async function addOne(produit) {
  if (produit.actual_qte < produit.qte) {
    produit.actual_qte++;
    await updateQuantity(produit);
  } else {
    console.log("Il n'y a plus de place!");
    alert("Il n'y a plus de place !");
  }
}

async function removeOne(produit) {
  if (produit.actual_qte > 0) {
    produit.actual_qte--;
    await updateQuantity(produit);
  } else {
    console.log("Désolé il n'y en a déja plus!");
    alert("Désolé il n'y en a déja plus!")

  }
}

async function updateQuantity(produit) {
  const fetchOptions = {
    method: "PUT",
    headers: {"Content-Type": "application/json"},
    body: JSON.stringify({id: produit.id, qte: produit.actual_qte})
  };
  try {
    const response = await fetch(url, fetchOptions);
    const dataJSON = await response.json();
    console.log(dataJSON);
    affichProduit();
  } catch (error) {
    console.error(error);
  }
}


function deleteProduit(idProduit) {
  const fetchOptions = {
    method: "DELETE",
  };
  fetch(url + "/" + idProduit, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      affichProduit();
    })
    .catch((error) => console.log(error));
}


</script>

<template>
  <div>
    <ProduitList @updateR="updateR"/>
  </div>

  <v-row>
    <v-col
      v-for="produit in listeProduit"
      :key="produit.id"
      cols="12"
      sm="6"
      md="4"
      lg="3"
    >
      <v-card class="product-card">
        <v-img
          :src="produit.photo"
          class="product-image"
          aspect-ratio="1"
        ></v-img>
        <v-card-title>{{ produit.nom }}</v-card-title>
        <v-card-text>
          <div class="product-details">
            <span class="product-quantity">Quantité: {{ produit.actual_qte }}</span>
            <div class="product-buttons">
              <v-btn @click="removeOne(produit)" class="qte_btna">- 1</v-btn>
              <v-btn @click="addOne(produit)" class="qte_btnb">+ 1</v-btn>
              <v-btn @click="deleteProduit(produit.id)" class="sup_btn">X</v-btn>
            </div>
          </div>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>


</template>

<style scoped>

.product-image img {
  width: 100%;
  height: auto;
}

.qte_btna, .qte_btnb {
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 50%;
  margin: 0 5px;
}

.sup_btn {
  position: absolute;
  top: 10px;
  right: 10px;
  color: red;
  height: 20px;
  width: 20px;
  border-radius: 50%;
}
</style>

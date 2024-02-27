<script setup>


const emit=defineEmits(['addProduit']);

let nom = "";
let qte = "";
let photo = "";

const handleSubmit = () => {
  emit('addProduit',nom, qte, photo);
};


</script>
<template>
  <div class="container">
    <form @submit.prevent="$emit('addProduit',nom,qte,photo)" class="form-container">
      <div class="input-container">
        <input class="add_bar" type="text" v-model="nom" placeholder=" Nom?" required/>
      </div>
      <div class="input-container">
        <input class="add_barq" type="number" v-model="qte" placeholder=" Choisis la quantité" required min="1"/>
      </div>



      <div class="input-container">

        <input class="add_barp" type="text" v-model="photo" placeholder=" Choisis une image catalogue ?"/>
      </div>

      <input class="add_btn" type="submit" value=" Ajouter "/>
    </form>
  </div>
</template>

<style scoped>
.container {
  display: flow;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.form-container {
  display: flex;
  flex-wrap: wrap;
}

.input-container {
  flex: 1;
  margin: 10px;
}

.add_bar, .add_barq, .add_barp {
  background-color: #f0f0f0;
  border: 1px solid #333;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
}

.add_btn {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add_btn:hover {
  background-color: #45a049;
}
.add_btn {
  margin-top: 100px;
  margin-left: 150px
}
</style>

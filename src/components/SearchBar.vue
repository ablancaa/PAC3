<template>
  <div class="search">
    <div>
    <form @submit.prevent="busqueda"> 
       <input type="text" id="consulta" v-model.trim="consulta1" placeholder="Search for a recipe" />
       <button v-if="consulta1 != ''" @click="clearSearch">Clear Search</button>
    </form>
    </div>
    
    <button @click="showForm">Add a new recipe</button>
  </div>
</template>
<script>

import { defineComponent, inject, ref } from "vue";
//import RecipeForm from "@/components/RecipeForm.vue";
export default defineComponent({
  name: "SearchBar",
   components: {
   //RecipeForm,
  },
  setup(){
    const receta = inject('recipe');
    const consulta1 = ref('');
    const busqueda = () => {
      if(consulta1.value === ''){
        console.log("está vacio");
       
        return
      }
     
     console.log(consulta1.value);
      
      const recipe = {
        consulta: consulta1.value,
      }

      receta.value.push(recipe);
      consulta1.value='';
      console.log("Objeto creado de busqueda: "+recipe.consulta);
    };
    console.log(receta.value);
    return {busqueda, consulta1}
  },
 data() {
    return {
      consulta: '',
      
    }
  },
  methods: {

  /* Aquest mètode s'encarregarà d'emetre un esdeveniment show-form. S’haurà
  d’executar quan es faci clic al botó “Add a new recipe”. */
  showForm(){
    this.$emit('openForm', this.showModal = true);
    console.log("Emitido de SearchBar: "+this.showModal);
  },
  /* Aquest mètode s'encarregarà de buidar l'element input del camp de cerca.
  S’haurà d’executar quan es faci clic al botó “Clear Search”. */
  clearSearch(){
       this.consulta = document.getElementById("consulta").value="";
       //this.consulta1 = '';
       console.log("Función clearSearch(){} Campo reseteado");
  },
   /*Aquest mètode s'executarà cada vegada que es modifiqui l'element
  input del camp de cerca (cada vegada que es teclegi una lletra). Emetrà un esdeveniment
  'search' amb el contingut del camp de cerca */
  search(newVal){
    this.page = 0;
    this.
    console.log(newVal);
  },
 }
});
</script>
<style scoped>
.search {
  width: 100%;
  padding: 15px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #ccc;
  margin-bottom: 25px;
  justify-content: space-between;
}
.search input {
  width: 100%;
  width: 500px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  margin: 0 auto;
  max-width: 500px;
}
.search button {
  margin-left: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  background: #4caf50;
  color: #fff;
}
</style>

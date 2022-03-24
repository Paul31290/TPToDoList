<script setup>
import Chose from "../Chose.js";
import ToDoListItem from './ToDoListItem.vue';
import ToDoForms from './ToDoForms.vue';
import { reactive, onMounted} from 'vue';
const listeC = reactive([]);

function handlerFaire(id, libelle, fait) {
    console.log(id, libelle, fait);
    let myHeaders =new Headers();
    myHeaders.append("Content-Type","application/json");
    const fetchOptions = {
        method: "PUT",
        headers: myHeaders,
        body: JSON.stringify({id:id, libelle:libelle, fait:!fait}),
    };

    fetch(url, fetchOptions)
    .then( (response) => {
        return response.json();
    })

    .then((dataJSON) => { 
        console.log(dataJSON); 
        getTodos()
    })

    .catch((error)=>{
        console.log(error)
    })
}
function handlerDelete(id) {
 console.log(id);
 const fetchOptions = {method: "DELETE"};
    fetch(url+"/"+id, fetchOptions)
    .then((response) => {
        return response.json();
    })
    .then((dataJSON) => {
        console.log(dataJSON);
        getTodos();  
    })

    .catch((error) => console.log(error));
}
function handlerAdd(libelle) {
    console.log(libelle)
    let myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");
        const fetchOptions = {
            method: "POST",
            headers: myHeaders,
            body: JSON.stringify({libelle:libelle}),
    };
    fetch(url, fetchOptions)
    .then( (response) => {
        return response.json();
    })

    .then((dataJSON) => { 
        console.log(dataJSON); 
        getTodos()
    })

    .catch((error)=>{
        console.log(error)
    })
}

const url =  "https://webmmi.iut-tlse3.fr/~pecatte/todos/public/24/todos";

onMounted(() => {
    console.log("onmounted")
    getTodos()
});
function getTodos(){
    const fetchOptions = {method: "GET"};
    fetch(url, fetchOptions)
    .then((response) => {
        return response.json();
    })
    .then((dataJSON) => {
        console.log(dataJSON);
        listeC.splice(0,listeC.length)
        dataJSON.forEach((v) => listeC.push(new Chose(v.id, v.libelle, v.fait)));
          
    })

    .catch((error) => console.log(error));
}

</script>

<template>
   <h3> Liste des choses à faire </h3>

    <ToDoForms 
        :libelle = "libelle"
        @addC = "handlerAdd"
    />

    <ToDoListItem
        v-for="(chose) of listeC"
        :key="[chose._id]"
        :chose = "chose"
        @eventSupprimer = "handlerDelete"
        @eventFaire = "handlerFaire"
    />
</template>

<style>

</style>

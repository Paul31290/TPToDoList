<script setup>
defineProps(["chose"]);
</script>

<template>
  
  <li>{{ chose.pourAfficher() }} 
    <button @click = "$emit('eventSupprimer', chose._id)">Supprimer</button>
    <button @click = "$emit('eventFaire', chose._id, chose._texte, chose._fait)">Faire</button>
  </li>
</template>

<style>

</style>
<script setup>
defineProps (["libelle"])
</script>

<template>
 <form @submit.prevent="$emit('addC', libelle)">
    <input type="text" v-model="libelle" placeholder="chose ?" />
    <input type="submit" value="valider" />
 </form>
</template>

<style>

</style>
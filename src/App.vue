<template>
    <input type="text" v-model="note"> 
    <button @click="sendToServer"> Enviar nota la servidor</button>
    <router-view></router-view>
</template>
  
<script lang="ts" setup>
  import { ref } from 'vue'

  let note = ref('')
  const sendToServer = async () => {
    const rawResponse = await fetch('http://localhost:3000/notes', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
        'Authorization': 'Bearer ' + localStorage.getItem('token')
      },
      body: JSON.stringify({ note: note.value })
    })

    const response = await rawResponse.json()
  }
</script>
  
<style scoped>
</style>
  
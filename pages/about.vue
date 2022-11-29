<script setup>

import { createClient } from '@supabase/supabase-js'
const supabase = createClient('https://uufrotxvcyajukeynncd.supabase.co', 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InV1ZnJvdHh2Y3lhanVrZXlubmNkIiwicm9sZSI6ImFub24iLCJpYXQiOjE2Njk1NDE1MTYsImV4cCI6MTk4NTExNzUxNn0.RYhetro9ENYiOnlUE4zk18M5OS0hzN_J_FfGp4FqkLQ');

const stage= reactive({
  obras: []
})

async function obtenerObras() {
  try {
    const { data, error } = await supabase
      .from("superheroes")
      .select("nombre, imagen")
      .order("id");
    let datos = data;
    stage.obras = datos;
    console.log("Obras: ", datos)
    console.log("stage: ", stage.obras)

  } catch (err) {
    console.error("Error retrieving data from db", err);
  }
}

onMounted(() => {
  obtenerObras();
})

</script>

<template>
  <h1>Hola about</h1>
    <div class="row justify-content-center">
      <BaseCard
        class="col-4 m-2"
        v-for="obra in stage.obras"
        :key="obra.id"
        :obra="obra"
      />
  </div>
</template>
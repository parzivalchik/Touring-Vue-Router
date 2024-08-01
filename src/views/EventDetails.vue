<script setup>
import EventService from "@/services/EventService.js";
import { computed, onMounted, ref } from "vue";

const props = defineProps(["id"]);

const event = ref("");
const id = computed(() => props.id);
onMounted(() => {
  EventService.getEvent(id.value)
    .then((response) => {
      event.value = response.data;
    })
    .catch((error) => {
      console.log(error);
    });
});
</script>

<template>
  <div v-if="event">
    <img 
      :src="event.organizer" 
      :alt="event.title" 
      style="width: 1000px; height: 400px; object-fit: cover;"
    />
    <h1>{{ event.title }}</h1>
    <p>Duration: {{ event.time }} Released: {{ event.date }} Watch on: {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

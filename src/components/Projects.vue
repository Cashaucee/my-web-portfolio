<script setup>
import { computed } from 'vue';
import ProjectCarousel from './ProjectCarousel.vue';
import projectsData from '../data/projects.json'; // Adjust this path to where your JSON file is located

const structuredDecks = computed(() => {
  const findProject = (id) => projectsData.find(p => p.id === id) || { id, title: 'Placeholder', description: '', image: './images/project-placeholder.jpg' };

  return [
    {
      id: "deck-ecommerce",
      carouselId: "carouselExampleDark",
      title: "E-Commerce Application",
      items: [findProject(1), findProject(4)] 
    },
    {
      id: "deck-course",
      carouselId: "carouselExampleDark1",
      title: "Course Booking Application",
      items: [findProject(2), findProject(3)]
    },
    {
      id: "deck-airline",
      carouselId: "carouselExampleDark2",
      title: "Airline Booking System",
      items: [findProject(5), findProject(6)]
    },
    {
      id: "deck-shortcourses",
      carouselId: "carouselExampleDark3",
      title: "Short Courses Capstone",
      items: [findProject(7), findProject(8), findProject(9)] 
    }
  ];
});
</script>

<template>
  <section id="projects" class="my-3 p-5">
    <div class="row mb-4">
      <div class="col-12">
        <h1 class="d-inline-block mb-4">My Projects</h1>
      </div>
    </div>
    
    <div class="row g-4">
      <ProjectCarousel 
        v-for="deck in structuredDecks"
        :key="deck.id"
        :carouselId="deck.carouselId"
        :categoryTitle="deck.title"
        :projectItems="deck.items"
      />
    </div>
  </section>
</template>
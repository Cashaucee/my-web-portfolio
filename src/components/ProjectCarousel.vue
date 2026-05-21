<script setup>
defineProps({
  carouselId: {
    type: String,
    required: true
  },
  categoryTitle: {
    type: String,
    required: true
  },
  projectItems: {
    type: Array,
    required: true
  }
});
</script>

<template>
  <div class="col-12 col-lg-6">
    <h2 class="d-inline-block mb-3">{{ categoryTitle }}</h2>
    
    <div :id="carouselId" class="carousel carousel-dark slide" data-bs-ride="carousel">
      
      <div class="carousel-indicators">
        <button 
          v-for="(item, index) in projectItems" 
          :key="'ind-' + carouselId + '-' + item.id"
          type="button" 
          :data-bs-target="'#' + carouselId" 
          :data-bs-slide-to="index" 
          :class="{ active: index === 0 }" 
          :aria-current="index === 0 ? 'true' : undefined"
          :aria-label="'Slide ' + (index + 1)"
        ></button>
      </div>
      
      <div class="carousel-inner">
        <div 
          v-for="(item, index) in projectItems" 
          :key="item.id"
          class="carousel-item" 
          :class="{ active: index === 0 }"
          data-bs-interval="10000"
        >
          <div class="carousel-title">
            <h5>{{ item.title }}</h5>
          </div>
          
          <img :src="item.image" :alt="item.title">
          
          <div class="carousel-caption d-md-block">
            <p>{{ item.description }}</p>
          </div>
        </div>
      </div>
      
      <button class="carousel-control-prev" type="button" :data-bs-target="'#' + carouselId" data-bs-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
      </button>
      <button class="carousel-control-next" type="button" :data-bs-target="'#' + carouselId" data-bs-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
      </button>
      
    </div>
  </div>
</template>
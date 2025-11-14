<template>
  <div class="card-slider">
    <span v-for="(item, index) in onlyFirstFew" :key="index">
      <div
        class="lable relative inline-block w-36 h-52 rounded-md shadow-md transition-transform duration-300 cursor-pointer"
        @click="goAnimePage(item)"
      >
        <img
          :src="item.images.webp.image_url"
          :alt="item.title"
          class="image w-full h-full object-cover rounded-md"
        />
        <div
          class="border-animation absolute inset-0 border-4 border-transparent rounded-md transition-all duration-500"
        ></div>
      </div>
    </span>
  </div>
</template>

<script setup>
import { computed, toRefs } from "vue";

const props = defineProps({
  topAnime: {
    type: Array,
    required: true,
  },
});

const { topAnime } = toRefs(props);

const onlyFirstFew = computed(() => {
  if (!topAnime.value) return [];
  return topAnime.value.slice(0, 9);
});
</script>

<style scoped>
.card-slider {
  margin: 60px auto;
  text-align: center;
}

/* Updated label class */
.lable {
  position: relative;
  margin: 0 -35px;
  width: 150px;
  height: 200px;
  border-radius: 5px;
  box-shadow: 0 10px 6px -6px #777;
  transform: skew(-20deg) rotate(-20deg);
  overflow: hidden; /* Ensure content is contained */
  cursor: pointer; /* Change cursor to pointer for interactivity */
}

/* Ensure the image is styled correctly */
.image {
  width: 100%; /* Ensure the image fills the container */
  height: 100%; /* Ensure the image fills the container */
  object-fit: cover; /* Maintain aspect ratio */
  border-radius: 5px; /* Match card corners */
  transition: transform 0.5s ease; /* Add smooth transition for image */
}

/* Border animation effect */
.border-animation {
  border-color: transparent;
  border-radius: 5px;
  transition: border-color 0.5s, border-width 0.5s; /* Add smooth transitions */
}

.lable:hover .border-animation {
  animation: border-animation 2s linear forwards; /* Apply animation */
  animation-delay: 0s; /* Start immediately on hover */
}

@keyframes border-animation {
  0% {
    border-width: 4px 0 0 0;
    border-color: green;
  }
  25% {
    border-width: 4px 4px 0 0;
    border-color: rgb(0, 102, 0);
  }
  50% {
    border-width: 4px 4px 4px 0;
    border-color: rgb(0, 87, 0);
  }
  75% {
    border-width: 4px 4px 4px 4px;
    border-color: rgb(0, 58, 0);
  }
  100% {
    border-width: 4px 4px 4px 4px;
    border-color: rgb(0, 27, 0);
  }
}

.lable:hover .image {
  transform: scale(1.05); /* Slightly scale up the image on hover */
}

.lable:hover {
  margin: 0 50px; /* Adjust margin on hover */
  transform: none; /* Reset skew on hover */
}

/* Extra class to control the animation */
.animation-delay {
  animation: border-animation 2s linear forwards; /* Animation for border */
  animation-delay: 2s; /* Delay before restarting the animation */
}
</style>
    
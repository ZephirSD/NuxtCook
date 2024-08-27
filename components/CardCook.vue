<template>
  <div class="card bg-primary text-primary-content w-80 shadow-xl">
    <figure class="px-10 pt-10">
      <img
        :src="meal.strMealThumb"
        alt="imgplat"
        class="rounded-xl"
      />
    </figure>
    <div class="card-body">
      <h2 class="card-title">{{ meal.strMeal }}</h2>
      <h3>Origin: {{ meal.strArea }}</h3>
      <div class="max-h-32 overflow-y-auto">{{ meal.strInstructions }}</div>
    </div>
  </div>
</template>

<script setup>
  const { meal } = defineProps(['meal']);
</script>

<template>
  <div class="md:container md:mx-auto">
    <div class="navbar bg-base-100 py-5">
      <div class="flex-1">
        <p class="text-3xl">NuxtCook</p>
      </div>
      <div class="flex-none gap-2">
        <div class="form-control">
          <input
            type="text"
            placeholder="Search"
            class="input input-bordered w-56"
            v-model="searchPlat"
            @change="fetchSearchMeal"
          />
        </div>
      </div>
    </div>
    <!-- Gestion du chargement et des erreurs -->
    <section v-if="loading" class="w-full flex justify-center items-center">
      <span class="loading loading-bars loading-lg"></span>
    </section>
    <section v-else-if="error" class="text-center my-4">
      <p>Erreur lors du chargement des plats.</p>
    </section>
    <!-- Grille des plats -->
    <section v-else class="grid grid-cols-1 w-full sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 my-4">
      <div v-for="plat in filteredPlats" :key="plat.idMeal" class="flex justify-center">
        <CardCook :meal="plat"/>
      </div>
    </section>
  </div>
</template>

<script setup>
const searchPlat = ref('');
const { data: plats, pending: loading, error, refresh } = await useFetch(`https://www.themealdb.com/api/json/v1/1/search.php?s=${searchPlat.value}`);
const fetchSearchMeal = async () => {
  await refresh();
};

const filteredPlats = computed(() => {
  if (!plats.value?.meals) {
    return [];
  }
  return plats.value.meals.filter(plat =>
    plat.strMeal.toLowerCase().includes(searchPlat.value.toLowerCase())
  );
});

</script>


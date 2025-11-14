<template>
  <div>
    <div class="header">
      <Navigation />
    </div>
    <div class="max-w-5xl shadow-md m-auto min-h-screen pt-3">
      <div class="px-2">
        <div class="topAnime">
          <div class="h-10 w-full bg-green-900">
            <h1 class="text-2xl px-4 text-white font-bold">Upcoming Anime:</h1>
          </div>
          <TopAnime :topAnime="topAnime"></TopAnime>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const topAnime = ref(null);

onBeforeMount(() => {
  getData();
});

onMounted(() => {
  getData();
});

async function getData() {
  try {
    const { data: result } = await useLazyFetch(
      "https://api.jikan.moe/v4/top/anime"
    );
    if (result.value) {
      topAnime.value = result.value.data;
    }
  } catch (error) {
    console.log(error);
  }
}
</script>

<style scoped>
</style>
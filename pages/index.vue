<script setup>
const { data } = await useAsyncData("blog", () =>
  queryContent("/").sort({ createdAt: 0 }).find()
);
</script>
<template>
  <div>
    <div v-for="blog in data" :key="blog.id">
      <NuxtLink :to="blog._path">
        <h1>{{ blog.title }}</h1>
      </NuxtLink>
      <h2>{{ blog.description }}</h2>
    </div>
  </div>
</template>

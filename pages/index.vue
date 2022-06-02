<script setup>
const { data } = await useAsyncData("blog", () =>
  queryContent("/blog").sort({ createdAt: 0 }).find()
);

const date = (value) =>
  new Date(value).toLocaleDateString("en-us", {
    month: "long",
    day: "numeric",
    year: "numeric",
  });

const blogs = data.value.map((blog) => ({
  ...blog,
  createdAt: date(blog.createdAt),
}));
</script>

<template>
  <div>
    <div v-for="blog in blogs" :key="blog.id">
      <NuxtLink :to="blog._path">
        <h1>{{ blog.title }}</h1>
      </NuxtLink>
      <h2>{{ blog.description }}</h2>
      <p>{{ blog.createdAt }}</p>
    </div>
  </div>
</template>

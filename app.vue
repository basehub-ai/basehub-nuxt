<template>
  <h1>{{ data?.blog._title }}</h1>

  <div v-for="post in data?.blog.posts.items" :key="post._id">
    <h2>{{ post._title }}</h2>
    <NuxtLink :to="`/posts/${post._slug}`">Read more</NuxtLink>
  </div>
</template>

<script setup lang="ts">
import { basehub } from "basehub";

const { data } = await useAsyncData("item", async () => {
  const data = await basehub().query({
    blog: {
      _title: true,
      posts: {
        items: {
          _id: true,
          _title: true,
          _slug: true,
        },
      },
    },
  });
  return data;
});
</script>

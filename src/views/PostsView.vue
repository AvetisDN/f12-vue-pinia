<script setup>
import { RouterLink } from "vue-router";
import { storeToRefs } from "pinia";
import { usePostStore } from "../stores/post";

const { posts, loading, error } = storeToRefs(usePostStore());
const { fetchPosts } = usePostStore();

fetchPosts();
</script>

<template>
  <div class="about">
    <h1>Posts feed</h1>
    <p v-if="loading">Loading...</p>
    <p v-if="error" class="error">{{ error.message }}</p>
    <div v-if="posts">
      <p v-for="post in posts" :key="post.id">
        <RouterLink :to="`/post/${post.id}`">{{ post.title }}</RouterLink>
      </p>
    </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    flex-direction: column;
    gap: 1rem;
  }
}
</style>

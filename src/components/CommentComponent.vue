<script setup>
defineProps(["comment"]);
</script>

<template>
  <div class="comments">
    <h3>{{ comment.name }}</h3>
    <p>{{ comment.body }}</p>
  </div>
</template>

<style>
.comments {
  font-size: 12px;
}
</style>

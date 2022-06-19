<script setup>
import { useRoute } from "vue-router";
import { storeToRefs } from "pinia";
import { useUserStore } from "../stores/user";
import { usePostStore } from "../stores/post";
import { useCommentStore } from "../stores/comment";
import CommentComponent from "../components/CommentComponent.vue";

const route = useRoute();
const { getPostUser } = storeToRefs(useUserStore());
const { fetchUsers } = useUserStore();
const { post, loading, error } = storeToRefs(usePostStore());
const { fetchPost } = usePostStore();
const { getPostComments } = storeToRefs(useCommentStore());
const { fetchComments } = useCommentStore();

fetchUsers();
fetchPost(route.params.id);
fetchComments();
</script>

<template>
  <div class="about">
    <p v-if="loading">Loading...</p>
    <p v-if="error" class="error">{{ error.message }}</p>
    <div v-if="post">
      <h1>{{ post.title }}</h1>
      <i> by {{ getPostUser.name }} </i>
      <p>{{ post.body }}</p>
      <hr />
      <h3>Comments ({{ getPostComments.length }})</h3>
      <CommentComponent
        v-for="comment in getPostComments"
        :key="comment.id"
        :comment="comment"
      />
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
  .about > div {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
}
</style>

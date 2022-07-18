<template lang="">
  <div class="alert alert-warning alert-dismissible fade show" role="alert">
    {{ message }}
    <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
  </div>
</template>
<script lang="ts" setup>
import { defineProps } from 'vue';

const props = defineProps({
  message: String,
});

props.message;
</script>
<style lang=""></style>

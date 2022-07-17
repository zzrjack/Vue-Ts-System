<template lang="">
  <div class="details container">
    <h1 class="page-header">
      <router-link class="btn btn-outline-success" to="/">返回</router-link>
      <span style="float: right">
        <router-link class="btn btn-primary" to="/edit/1">编辑</router-link>
        &nbsp;&nbsp;
        <button type="button" class="btn btn-danger">删除</button>
      </span>
    </h1>
  </div>
</template>
<script lang="ts">
import { useRoute } from 'vue-router';
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';
import { Customer } from '@/utils/types';
export default {
  setup() {
    const route = useRoute();
    const customer = ref<Customer>();
    onMounted(async () => {
      const res = await axios.get('http://localhost:3000/users/' + route.params.id);
      //console.log(res.data);
      customer.value = res.data;
    });
    return { customer };
  },
};
</script>
<style lang=""></style>

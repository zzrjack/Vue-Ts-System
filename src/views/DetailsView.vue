<template lang="">
  <div class="details container">
    <h1 class="page-header">
      <router-link class="btn btn-outline-success" to="/">返回</router-link>
      <span style="float: right">
        <router-link class="btn btn-primary" :to="'/edit/' + customer.id">编辑</router-link>
        &nbsp;&nbsp;
        <button type="button" class="btn btn-danger" @click="deleteCustomer(customer.id)">
          删除
        </button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item">
        <i class="fa-solid fa-user"></i>&nbsp;&nbsp;{{ customer.name }}
      </li>
      <li class="list-group-item">
        <i class="fa-solid fa-phone"></i>&nbsp;&nbsp;{{ customer.phone }}
      </li>
      <li class="list-group-item">
        <i class="fa-solid fa-envelope"></i>&nbsp;&nbsp;{{ customer.email }}
      </li>
      <li class="list-group-item">
        <i class="fa-solid fa-graduation-cap"></i>&nbsp;&nbsp;{{ customer.education }}
      </li>
      <li class="list-group-item">
        <i class="fa-solid fa-school"></i>&nbsp;&nbsp;{{ customer.graduationschool }}
      </li>
      <li class="list-group-item">
        <i class="fa-solid fa-user-tie"></i>&nbsp;&nbsp;{{ customer.profession }}
      </li>
      <li class="list-group-item">
        <i class="fa-regular fa-paper-plane"></i>&nbsp;&nbsp;{{ customer.profile }}
      </li>
    </ul>
  </div>
</template>
<script lang="ts">
import { useRoute } from 'vue-router';
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';
import { Customer } from '@/utils/types';
import router from '@/router';
export default defineComponent({
  setup() {
    const route = useRoute();
    const customer = ref<Customer>({
      name: '',
      phone: '',
      email: '',
      education: '',
      graduationschool: '',
      profession: '',
      profile: '',
      id: '',
    });
    onMounted(async () => {
      const res = await axios.get('http://localhost:3000/users/' + route.params.id);
      //console.log(res.data);
      customer.value = res.data;
    });
    const deleteCustomer = async () => {
      await axios.delete('http://localhost:3000/users/' + route.params.id);
      router.push('/');
    };
    return { customer, deleteCustomer };
  },
});
</script>
<style lang=""></style>

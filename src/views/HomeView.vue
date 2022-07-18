<template>
  <div class="home container">
    <!-- 表格 -->
    <AlertComponet v-if="alert" :message="alert" />
    <input type="text" class="form-control" placeholder="search..." v-model="filterInput" />
    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">姓名</th>
          <th scope="col">电话</th>
          <th scope="col">邮箱</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="customer in fileterBy(customers, filterInput)" :key="customer.id">
          <th scope="row">{{ customer.id }}</th>
          <td>{{ customer.name }}</td>
          <td>{{ customer.phone }}</td>
          <td>{{ customer.email }}</td>
          <td>
            <router-link
              class="btn btn-outline-secondary"
              aria-current="page"
              :to="'/details/' + customer.id"
              >详情</router-link
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
export default {
  name: 'HomeView',
};
</script>

<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { Customer } from '@/utils/types';
import AlertComponet from '../components/AlertComponet.vue';
import { useRoute } from 'vue-router';
const filterInput = ref<string>('');
const alert = ref<string>('');
const customers = ref<Customer[]>([]);
const route = useRoute();
console.log(route);
if (route.query.alert) {
  alert.value = String(route.query.alert);
  setTimeout(() => {
    alert.value = '';
  }, 2000);
}
// 发起请求
onMounted(async () => {
  const res = await axios.get('http://localhost:3000/users');
  // console.log(res);
  customers.value = res.data;
});
const fileterBy = (customers: Customer[], value: string) => {
  return customers.filter((customer: Customer) => customer.name.match(value));
};
</script>

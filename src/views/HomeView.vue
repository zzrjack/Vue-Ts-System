<template>
  <div class="home container">
    <!-- 表格 -->
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
        <tr v-for="customer in customers" :key="customer.id">
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
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';
import { Customer } from '@/utils/types';
export default defineComponent({
  name: 'HomeView',
  components: {},
  setup() {
    const customers = ref<Customer[]>([]);
    // 发起请求
    onMounted(async () => {
      const res = await axios.get('http://localhost:3000/users');
      // console.log(res);
      customers.value = res.data;
    });
    return { customers };
  },
});
</script>

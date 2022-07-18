<template>
  <div class="edit container">
    <form @submit.prevent="updateCustomer()">
      <div class="mb-3">
        <label class="form-label">姓名</label>
        <input type="text" class="form-control" placeholder="name..." v-model="customer.name" />
      </div>
      <div class="mb-3">
        <label class="form-label">电话</label>
        <input type="text" class="form-control" placeholder="phone..." v-model="customer.phone" />
      </div>
      <div class="mb-3">
        <label class="form-label">邮箱</label>
        <input type="email" class="form-control" placeholder="email..." v-model="customer.email" />
      </div>
      <div class="mb-3">
        <label class="form-label">学历</label>
        <input
          type="text"
          class="form-control"
          placeholder="education..."
          v-model="customer.education"
        />
      </div>
      <div class="mb-3">
        <label class="form-label">毕业学校</label>
        <input
          type="text"
          class="form-control"
          placeholder="graduation shcool..."
          v-model="customer.graduationschool"
        />
      </div>
      <div class="mb-3">
        <label class="form-label">专业</label>
        <input
          type="text"
          class="form-control"
          placeholder="profession..."
          v-model="customer.profession"
        />
      </div>
      <div class="form-group">
        <label>个人简介</label>
        <textarea class="form-control" rows="3" v-model="customer.profile"></textarea>
      </div>
      <div class="d-grid gap-2">
        <button class="btn btn-primary" type="submit" style="margin-top: 24px">更新</button>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
export default {
  name: 'EditView',
};
</script>

<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { useRoute, useRouter } from 'vue-router';
import { Customer } from '@/utils/types';

const route = useRoute();
const router = useRouter();
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
  // console.log(res);
  customer.value = res.data;
});
const updateCustomer = async () => {
  //console.log(customer.value);
  let uCustomer = {
    name: customer.value.name,
    phone: customer.value.phone,
    email: customer.value.email,
    education: customer.value.education,
    graduationschool: customer.value.graduationschool,
    profession: customer.value.profession,
    profile: customer.value.profile,
  };
  await axios.put('http://localhost:3000/users/' + route.params.id, uCustomer);
  router.push({ path: '/', query: { alert: '用户信息已更新' } });
};
</script>

<template>
  <div class="add container">
    <form @submit.prevent="addCustomer()">
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
          v-model="customer.graduationshcool"
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
        <button class="btn btn-primary" type="submit" style="margin-top: 24px">添加</button>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';
import { Customer } from '@/utils/types';
export default defineComponent({
  name: 'AddView',
  components: {},
  setup() {
    const router = useRouter();
    const customer = ref<Customer>({
      name: '',
      phone: '',
      email: '',
      education: '',
      graduationshcool: '',
      profession: '',
      profile: '',
      id: '',
    });
    const addCustomer = async () => {
      //console.log(customer.value);
      let newCustomer = {
        name: customer.value.name,
        phone: customer.value.phone,
        email: customer.value.email,
        education: customer.value.education,
        graduationchool: customer.value.graduationshcool,
        profession: customer.value.profession,
        profile: customer.value.profile,
      };
      const res = await axios.post('http://localhost:3000/users', newCustomer);
      //console.log(res);
      router.push('/');
    };
    return { customer, addCustomer };
  },
});
</script>

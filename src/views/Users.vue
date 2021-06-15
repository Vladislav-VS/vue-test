<template>
  <div>
    <div>
      <ol>
        <User :user="user" v-for="user in users" :key="user.id"/>
      </ol>
    </div>
    <div>
      <ButtonPageSelector v-on:updateUsers="foo" getInformationPage="getInformationPage" :per_page="per_page"
                          :page="page" :users="users" v-for="page in pages" :key="page"/>
    </div>
    <div>
      Количество пользователей на странице
      <input v-model="per_page" :placeholder="per_page">
      <button @click="changePerPage(page, per_page)">Изменить</button>
    </div>
  </div>
</template>

<script>
import User from './User.vue'
import axios from 'axios'
import ButtonPageSelector from './ButtonPageSelector.vue'
import {defineComponent, onMounted, ref} from "@vue/composition-api";


export default defineComponent({
  components: {
    User,
    ButtonPageSelector
  },
  setup() {
    let page = ref(1);
    let users = ref([]);
    let pages = ref([1, 2]);
    let per_page = ref(6);
    let foo = (p) => {
      getInformationPage(p,per_page.value);
    }
    let getInformationPage = (p) => {
      axios.get('https://reqres.in/api/users?page=' + p + '&per_page=' + per_page.value)
          .then(response => {
            users.value = response.data.data;
            per_page.value = response.data.per_page;
            page.value = response.data.page;
            pages.value = response.data.total_pages;
          })
    }
    let changePerPage = (p, per_page) => {
      getInformationPage(p,per_page);
    }
    onMounted(() => {
      getInformationPage(page.value);
    });

    return {
      page,
      pages,
      users,
      foo,
      per_page,
      getInformationPage,
      changePerPage
    }
  },


})

</script>

<style>
</style>

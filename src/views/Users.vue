<template>
  <div>
    <div>
      <ol>
        <User :user="user" v-for="user in users" :key="user.id"/>
      </ol>
    </div>
    <div>
    <ButtonPageSelector v-on:updateUsers="foo" :page="page" :users="users" v-for="page in pages" :key="page"/>
    </div>
  </div>
</template>

<script>
import User from './User.vue'
import axios from 'axios'
import ButtonPageSelector from './ButtonPageSelector.vue'
import {defineComponent, onMounted, reactive, ref} from "@vue/composition-api";


export default defineComponent({
  components: {
    User,
    ButtonPageSelector
  },
   setup() {
    let page = ref(1);
    let users = reactive([]);
    let pages = reactive([1,2]);
    let foo = (userArr) => {
      users = userArr;
    }

     onMounted(() => {
       axios
           .get('https://reqres.in/api/users?page=1')
           .then(response => {
             users = response.data.data;
             page = response.data.page;
             pages = response.data.total_pages;
           })
     });

    return {
      page,
      pages,
      users,
      foo
    }
  },



})

</script>

<style>
</style>

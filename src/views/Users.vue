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

export default {
  /*ыуегз() {
    let foo1 = ref(j);
    let foo2 = reactive({val: 33});
    let method = (userArr) => {
      this.users = userArr;
    }


    return {
      foo1,
      foo2,
      method
    }
  },*/
  components: {
    User,
    ButtonPageSelector
  },
  data() {
    return {
      users: [],
      page: 1,
      pages: []
    }
  },
  mounted() {
    axios
        .get('https://reqres.in/api/users?page=1')
        .then(response => {
          this.users = response.data.data;
          this.page = response.data.page;
          this.pages = response.data.total_pages;
        })
  },
  methods: {
    foo (userArr) {
      this.users = userArr;
    }
  }

}

</script>

<style>
</style>

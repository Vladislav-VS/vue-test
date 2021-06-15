<template>
  <div v-bind:class="{contact:true}">
    <div>
      {{ currentUser.var.first_name }} {{ currentUser.var.last_name }}
    </div>
    <div>
      {{ currentUser.var.email }}
    </div>
    <img :src="currentUser.var.avatar"/>
    <div>
    </div>
    {{supportUser.var.text}}
    <div>

    </div>
    <a :href="supportUser.var.url">Поддержка</a>
    <div>
      <router-link :to="'/'">К списку пользователей</router-link>
    </div>
  </div>
</template>

<script>
import {defineComponent, onMounted, reactive} from "@vue/composition-api";
import axios from "axios";

export default defineComponent({

  setup(props, ctx) {
    let currentUser = reactive({var: {}});
    let supportUser = reactive({var: {}});
    let id = ctx.root.$route.params.id;
    onMounted(() => {
      axios.get('https://reqres.in/api/users/' + id)
          .then(response => {
            currentUser.var = response.data.data;
            supportUser.var = response.data.support;
            console.log(supportUser.var)
          })
    });
    return {
      currentUser,
      supportUser
    }
  }
})
</script>

<style scoped>

</style>
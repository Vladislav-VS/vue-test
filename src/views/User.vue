<template>
  <div v-bind:class="{contact:true, contactClick: showEmail}" v-on:click="showUserEmail">
    <div>
      {{ currentUser.first_name }} {{ currentUser.last_name }}
    </div>
    <div v-if="showEmail">
      {{ currentUser.email }}
    </div>
    <img :src="currentUser.avatar"/>
    <div>
      <router-link :to="'/' + currentUser.id">Подробнее</router-link>
    </div>
  </div>
</template>

<script>
import {computed, ref} from "@vue/composition-api";

export default {
  props: {
    user: Object
  },
  setup(props) {
    let currentUser = computed(() => props.user);
    let showEmail = ref(false);
    let showUserEmail = () => {
      showEmail.value = !showEmail.value;
    }

    // let fatUserClick = () => {
    //     ctx.root.$router.push({name: 'FatUser', params: {id: props.id}});
    // }

    return {
      showEmail,
      showUserEmail,
      currentUser
    }
  }
}
</script>

<style scoped>
.contact {
  background-color: antiquewhite;
  margin: auto;
  margin-bottom: 5%;
  border: 5px double #42b983;
  padding: 3%;
  border-radius: 40px;
  text-align: center;
  width: 60%;
}

.contactClick {
  background-color: burlywood;
}
</style>
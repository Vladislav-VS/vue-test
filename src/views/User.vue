<template>
  <div v-bind:class="{contact:true, contactClick: showEmail}"   v-on:click="showUserEmail">
    <div>
      {{ user.first_name }} {{ user.last_name }}
    </div>
    <div v-if="showEmail">
        {{ user.email }}
      </div>
    <img :src="user.avatar"/>
  </div>
</template>

<script>
export default {
  name: "User",
  data() {
    return {
      showEmail: false
    }
  },
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  methods: {
    showUserEmail() {
      this.showEmail = !this.showEmail;
    }
  }
}
</script>

<style scoped>
  .contact{
    background-color: antiquewhite;
    margin: auto;
    margin-bottom: 5%;
    border: 5px double #42b983 ;
    padding: 3%;
    border-radius: 40px;
    text-align: center;
    width: 60%;
  }

  .contactClick{
    background-color: burlywood;
  }
</style>
<template>
  <button @click="goToThisPage">
    {{ p }}
  </button>
</template>

<script>
import axios from "axios";
import {defineComponent, getCurrentInstance} from "@vue/composition-api";
// import {ref} from "@vue/composition-api";

export default defineComponent({
  props: {
    page: Number
  },
  setup(props) {
    const {emit} = getCurrentInstance();

    let p = props.page;// let users = reactive(props.users);
    let goToThisPage = () => {
      axios.get('https://reqres.in/api/users?page=' + p).then(response => {
        console.log(""+response);
        emit('updateUsers', response.data.data)
        // this.$emit('updateUsers', response.data.data)
      })
    }
    return {
      p,
      // page,
      // users,
      goToThisPage
    }
  /*props: {
    page: {
      type: Number,
      required: true
    },
    users: {
      type: Array,
      required: true
    },
  },
  methods: {
    goToThisPage() {
      axios.get('https://reqres.in/api/users?page=' + this.page).then(response => {
        this.$emit('updateUsers', response.data.data)
      })
    }*/
  }
})
</script>

<style scoped>

</style>
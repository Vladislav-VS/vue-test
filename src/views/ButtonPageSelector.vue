<template>
  <button @click="goToThisPage">
    {{ page }}
  </button>
</template>

<script>
import axios from "axios";

export default {
  name: "ButtonPageSelector",
  props: {
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
    }
  }
}
</script>

<style scoped>

</style>
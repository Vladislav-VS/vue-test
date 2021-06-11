<template>
  <button @click="goToThisPage(p)">
    {{ p }}
  </button>
</template>

<script>
import {computed, defineComponent, getCurrentInstance} from "@vue/composition-api";

export default defineComponent({
      props: {
        page: Number,
},
      setup(props) {
        const {emit} = getCurrentInstance();
        let p = computed(() => props.page)
        //let per_page = computed(() => props.per_page)
        let goToThisPage = () => {
          emit('updateUsers', p.value);
        }
        return {
          p,
          goToThisPage
        }
      },
    }
)
</script>

<style scoped>

</style>
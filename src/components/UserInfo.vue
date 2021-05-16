<template>
<div class="info">
  <p v-for="(value, key, index) in userLocation" :key="index">
    <strong>{{ key }}</strong> : {{ value }}
  </p>
</div>
</template>

<script>
import { useStore } from "vuex";
import { computed } from "vue";
export default {
name: "UserInfo",
  props: {
    username: {
      type: String,
      required: true
    }
  },
  setup(props){
    const store = useStore();
    const user = computed(() => store.state.users.find( user => user.login.username === props.username))
    const userLocation = computed(() => {
      const {city, country, postcode, state } = user.value.location
      return {city, country, postcode, state }
    });
    return {
      userLocation
    }
  }
}
</script>

<style scoped>
.info {
  padding: 1rem;
}
</style>
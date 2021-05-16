<template>
  <main>
    <article class="users">
      <section
          class="users__item"
          v-for="user in users"
          :key="user.login.uuid"
      >
        <RouterLink :to="`/users/${user.login.username}`">
          <div class="fade">
            {{ fullName(user) }}
          </div>
          <img
              class="user__thumbnail"
              :src="user.picture.medium"
              :alt="user.name.first"
          />
        </RouterLink>
      </section>
    </article>
  </main>
</template>

<script>
import {useStore} from "vuex";
import {computed} from "vue";

export default {
  name: "AppUserList",
  components: {},
  setup() {
    const store = useStore();
    const users = computed(() => store.state.users);
    const fullName = (user) => `${user.name.first} ${user.name.last}`
    return {
      users,
      fullName
    }
  }
};
</script>

<style scoped>
.users {
  padding-top: 7.5rem;
  display: grid;
  grid-gap: 0.5rem;
  grid:
    repeat(auto-fill, minmax(10rem, 1fr))
    / repeat(auto-fill, minmax(10rem, 1fr));
  grid-auto-rows: minmax(10rem, 1fr);
}

.user__thumbnail {
  width: 100%;
  display: block;
  height: auto;
}

.users__item {
  position: relative;
  cursor: pointer;
}

.fade {
  position: absolute;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease-in-out;
}

.users__item:hover .fade {
  opacity: 1;
  visibility: visible;
}
</style>
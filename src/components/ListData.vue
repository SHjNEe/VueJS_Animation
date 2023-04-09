<template>
  <div>
    <ul>
      <transition-group tag="ul" name="user-list">
        <li v-for="user in users" :key="user" @click="removeUser(user)">
          {{ user }}
        </li>
      </transition-group>
    </ul>
    <div>
      <input type="text" ref="userNameInput" />
      <button @click="addUser">Add Users</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: ["Max", "Manu", "Julie", "Angela", "Michael"],
    };
  },

  mounted() {},

  methods: {
    removeUser(user) {
      this.users = this.users.filter((usr) => usr !== user);
    },
    addUser() {
      const enteredUserName = this.$refs.userNameInput.value;
      this.users.unshift(enteredUserName);
      this.$refs.userNameInput.value = "";
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
li {
  border: 1px solid #ccc;
  padding: 1rem;
  text-align: center;
}
.user-list-enter-from,
.user-list-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}
.user-list-enter-active {
  transition: all 1s;
}
.user-list-leave-active {
  transition: all 1s;
  position: absolute;
}
.user-list-enter-to,
.user-list-leave-from {
  opacity: 1;
  transform: translateX(0);
}

.user-list-move {
  transition: transform 0.5s ease;
}
</style>

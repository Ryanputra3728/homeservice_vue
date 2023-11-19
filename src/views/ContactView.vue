<template>
  <div class="container">
    <h1 class="mt-5 mb-4">User List</h1>
    <div class="row">
      <div v-for="user in users" :key="user.id" class="col-md-4">
        <div class="user-card mb-4">
          <h3>{{ user.name }}</h3>
          <p>Email: {{ user.email }}</p>
          <p>Username: {{ user.username }}</p>
          <p>Phone: {{ user.phone }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      users: [],
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get("https://dummyjson.com/users");
        this.users = response.data.users;
      } catch (error) {
        console.error("Error fetching user data:", error);
      }
    },
  },
};
</script>

<style scoped>
.user-card {
  text-align: center;
  border: 1px solid #ccc;
  padding: 15px;
  transition: border-color 0.3s ease-in-out;
}

.user-card:hover {
  border-color: #007bff; /* Change this to the desired hover color */
}
</style>

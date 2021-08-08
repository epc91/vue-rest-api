<template>
  <div id="app" class="container">
    <!-- Row #1 -->
    <div class="row">
      <div class="col-md-12 mt-2">
        <h1>Users</h1>
      </div>
    </div>
    <!-- Row #2 -->
    <div class="row">
      <div class="col-md-12">
        <!-- Render Users Table Component -->
        <users-table :users='users'/>
      </div>
    </div>
  </div>
</template>

<script>
import UsersTable from '@/components/UsersTable.vue';

export default {
  name: 'app',
  data () {
    return {
      users: [],
    }
  },
  components: {
    UsersTable,
  },
  methods: {
    async getUsers() {
      // Method to get the list of users
      try {
        // We get the data using await
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        // Response in JSON format
        this.users = await response.json();
      } catch(error) {
        // Execution in case of error
        console.error(error);
      }
    },
    async postUser(user) {
      // Method to create a user
      try {
        // We get the data using await
        const response = await fetch('https://jsonplaceholder.typicode.com/users', {
          method: 'POST',
          body: JSON.stringify(user),
          headers: {'Content-Type': 'application/json; charset=UTF-8'},
        });
        // Response in JSON format
        const createdUser = await response.json();
        // Here we process the data
        this.users = [...this.users, createdUser];
      } catch(error) {
        // Execution in case of error
        console.error(error);
      }
    },
    async putUser(user) {
      // Method to update a user
      try {
        // We get the data using await
        const response = await fetch(`https://jsonplaceholder.typicode.com/users/${user.id}`, {
          method: 'PUT',
          body: JSON.stringify(user),
          headers: {'Content-Type': 'application/json; charset=UTF-8'},
        })
        // Response in JSON format
        const updatedUser = await response.json();
        // Here we process the data
        this.users = this.users.map(u => (u.id === user.id ? updatedUser : u))
      } catch(error) {
        // Execution in case of error
        console.error(error);
      }
    },
    async deleteUser(user) {
      // Method to delete a user
      try {
        // We get the data using await
        await fetch(`https://jsonplaceholder.typicode.com/usuarios/${user.id}`, {
          method: 'DELETE'
        });
        // Here we process the data
        this.users = this.users.filter(u => u.id !== user.id);
      } catch(error) {
        // Execution in case of error
        console.error(error);
      }
    }
  },
  mounted() {
    this.getUsers();
  }
}
</script>
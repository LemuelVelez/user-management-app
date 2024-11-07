<template>
  <div class="container mx-auto p-6">
    <!-- Add User Form -->
    <AddUserForm :onSave="saveUser" />

    <!-- Update User Form -->
    <UpdateUserForm 
      :user="selectedUserForUpdate" 
      :onUpdate="updateUser" 
      v-if="selectedUserForUpdate"
    />

    <div class="mt-6">
      <UserCard 
        v-for="user in users" 
        :key="user.email" 
        :user="user" 
        :onDelete="deleteUser" 
        :onUpdate="setUserForUpdate"
      />
    </div>
  </div>
</template>

<script>
import AddUserForm from './components/AddUserForm.vue'
import UpdateUserForm from './components/UpdateUserForm.vue'
import UserCard from './components/UserCard.vue'
import Swal from 'sweetalert2'

export default {
  components: { AddUserForm, UpdateUserForm, UserCard },
  data() {
    return {
      users: [],  // List of all users
      selectedUserForUpdate: null // User selected for update
    }
  },
  methods: {
    saveUser(user) {
      // Add new user if name and email are provided
      if (user.name && user.email) {
        this.users.push({ ...user });
        Swal.fire('Success', 'User saved successfully!', 'success');
      } else {
        Swal.fire('Error', 'Please fill out all fields.', 'error');
      }
    },
    deleteUser(user) {
      // Remove user from the users array
      const index = this.users.indexOf(user);
      if (index !== -1) {
        this.users.splice(index, 1);
        Swal.fire('Deleted!', 'User has been deleted.', 'success');
      }
    },
    setUserForUpdate(user) {
      // Set the user data for updating, will populate the update form
      this.selectedUserForUpdate = { ...user };
    },
    updateUser(user) {
      // Find the user to update in the array based on email
      const index = this.users.findIndex(u => u.email === user.email);
      if (index !== -1) {
        // Replace old user data with new updated data
        this.users.splice(index, 1, { ...user });
        Swal.fire('Updated!', 'User has been updated successfully!', 'success');
        this.selectedUserForUpdate = null; // Reset the form after update
      } else {
        Swal.fire('Error', 'User not found for update.', 'error');
      }
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 1200px;
}
</style>

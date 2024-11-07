<template>
  <div class="w-full max-w-xs p-4 bg-white shadow-md rounded-md">
    <h2 class="text-center font-semibold text-xl mb-4">Add New User</h2>
    <form @submit.prevent="handleSubmit">
      <!-- Name input with icon -->
      <div class="flex items-center mb-3 border rounded">
        <i class="fas fa-user p-2"></i>
        <input 
          type="text" 
          v-model="newUser.name" 
          placeholder="Name" 
          class="w-full p-2 border-none"
          required
        />
      </div>
      
      <!-- Email input with icon -->
      <div class="flex items-center mb-3 border rounded">
        <i class="fas fa-envelope p-2"></i>
        <input 
          type="email" 
          v-model="newUser.email" 
          placeholder="Email" 
          class="w-full p-2 border-none"
          required
        />
      </div>

      <!-- Submit button with icon -->
      <button type="submit" class="w-full p-2 bg-blue-500 text-white rounded flex items-center justify-center">
        <i class="fas fa-save mr-2"></i> Save User
      </button>
    </form>
  </div>
</template>

<script>
// Import SweetAlert2
import Swal from 'sweetalert2';

export default {
  props: ['onSave'],
  data() {
    return {
      newUser: { name: '', email: '' }
    };
  },
  methods: {
    handleSubmit() {
      if (this.newUser.name && this.newUser.email) {
        this.onSave(this.newUser); // Trigger the save method passed from parent
        this.resetForm();
      } else {
        Swal.fire('Error', 'Please fill out all fields.', 'error');
      }
    },
    resetForm() {
      // Reset the form fields after adding a user
      this.newUser = { name: '', email: '' };
    }
  }
}
</script>

<!-- Add Font Awesome CDN for icons -->
<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css');
</style>

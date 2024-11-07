<template>
    <div class="p-4 bg-gradient-to-r from-gray-100 via-gray-300 to-gray-500 shadow-md rounded-md my-2">
      <p class="font-semibold text-gray-800">{{ user.name }}</p>
      <p class="text-sm text-gray-600">{{ user.email }}</p>
  
      <!-- Delete button with icon -->
      <button 
        @click="handleDelete" 
        class="mt-2 px-4 py-1 bg-red-500 text-white rounded flex items-center justify-center">
        <i class="fas fa-trash-alt mr-2"></i> Delete
      </button>
  
      <!-- Update button with icon -->
      <button 
        @click="handleUpdate" 
        class="mt-2 px-4 py-1 bg-yellow-500 text-white rounded flex items-center justify-center">
        <i class="fas fa-edit mr-2"></i> Update
      </button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['user', 'onDelete', 'onUpdate'],
    methods: {
      handleDelete() {
        this.onDelete(this.user);
      },
      handleUpdate() {
        // Trigger the onUpdate method, passing the user data to be updated
        this.onUpdate(this.user);
      }
    }
  }
  </script>
  
  <!-- Add Font Awesome CDN for icons -->
  <style scoped>
  @import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css');
  </style>
  
<script setup lang="ts">
const user=useSupabaseUser();

const links = [
  [{
    label: 'Home',
    icon: 'i-heroicons-home',
    to: '/index'
  }], 
  
  [{
    label: 'Login',
    icon: 'material-symbols:person',
    to: '/login'
  }]
]
</script>

<template>
  <UHorizontalNavigation :links="links" class="border-b border-gray-200 dark:border-gray-800" />
</template>
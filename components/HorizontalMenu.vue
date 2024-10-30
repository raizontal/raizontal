<script setup lang="ts">
const user=useSupabaseUser();
const auth=useSupabaseClient().auth;
async function logout(){
  const {error} = await auth.signOut() 

        if(error)
            console.log(error.message)
        else
            navigateTo('/login');
}
const links = [
  [{
    label: 'Home',
    icon: 'i-heroicons-home',
    to: '/index'
  }],
  
  
]
</script>

<template>
  <div class="flex justify-end border-b">
    <UHorizontalNavigation :links="links" class="border-b border-gray-200 dark:border-gray-800" />
    <UButton v-if="user" @click="logout()" color="primary" variant="link">Logout</UButton>
    <ColorMode/>
  </div>
  
</template>

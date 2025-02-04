<script lang="ts" setup>
  const user = useSupabaseUser()
  console.log(user.value?.email)
  const logout = async()=>{
    const {error} = await useSupabaseClient().auth.signOut()
    if(error) return
    navigateTo('/login')
  }
</script>
<template>
  <Button @click="logout">Logout</Button>
  <Icon name="uil:github"/>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>

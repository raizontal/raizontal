<script setup lang="ts">


import { watchDebounced } from '@vueuse/core';

interface LoginForm {
    email: string
    password: string 
}
const supabase = useSupabaseClient()
const formData = ref ({
  email: '',
  password: '',
})


const login = async(formData: LoginForm)=>{
    const { error } = await supabase.auth.signInWithPassword({
      email: formData.email,
      password: formData.password
    })
      
    return { error }
}



watchDebounced(formData, () => {
  
}, { debounce: 1000, deep: true })

const signin = async()=>{
  const { error } = await login(formData.value)
  if(error) showError(error.message)
  if(!error) return navigateTo('/')

}


</script>

<template>
    <div class="mx-auto flex w-full justify-center items-center p-10 text-center -mt-20 min-h-[90vh]">
      <Card class="max-w-sm w-full mx-auto">
        <CardHeader>
          <CardTitle class="text-2xl"> 
            <div class="flex justify-center">
                Inicio sesión
            </div>
          </CardTitle>
          <CardDescription> Login to your account </CardDescription>
        </CardHeader>
        <CardContent>
          <div class="flex flex-col gap-4 mb-4 justify-center items-center">
            <Button variant="outline" class="w-full"> Register with Google </Button>
            <Separator label="Or" />
          </div>
  
          <form class="grid gap-4" @submit.prevent="signin">
            <div class="grid gap-2">
              <Label id="email" class="text-left">Email</Label>
              <Input 
              v-model="formData.email" 
                type="email" 
                placeholder="johndoe19@example.com" 
                required 
                />
              <!-- <ul class="text-sm text-left text-red-500" v-if="realTimeErrors?.email.length">
                <li v-for="error in realTimeErrors.email" :key="error" class="list-disc">
                  {{ error }}
                </li>
              </ul> -->
            </div>
            <div class="grid gap-2">
              <div class="flex items-center">
                <Label id="password">Password</Label>
                <a href="#" class="inline-block ml-auto text-xs underline"> Forgot your password? </a>
              </div>
              <Input  id="password" v-model="formData.password" type="password" autocomplete required  />
              
            </div>
            
            <Button type="submit" class="w-full"> Login </Button>
          </form>
          <div class="mt-4 text-sm text-center">
            Don't have an account?
          </div>
        </CardContent>
      </Card>
    </div>
  </template>
<script setup lang="ts">
import { object, string, type InferType } from 'yup'
import type { FormSubmitEvent } from '#ui/types'
const auth = useSupabaseClient().auth
const schema = object({
  email: string().email('Email inválido').required('Requerido'),
  password: string()
    .min(8, 'Debe tener al menos 8 carácteres')
    .required('Requerido')
})

type Schema = InferType<typeof schema>

const state = reactive({
  email: undefined,
  password: undefined
})

async function onSubmit(event: FormSubmitEvent<Schema>) {
  // Do something with event.data
  const {error} = await auth.signInWithPassword({
            email: event.data.email,
            password: event.data.password,
        }) 
    if(error)
        console.log(error)
    else
        navigateTo('/');
}
</script>

<template>
  <UForm :schema="schema" :state="state" class="space-y-4" @submit="onSubmit">
    <UFormGroup label="Email" name="email">
      <UInput v-model="state.email" />
    </UFormGroup>

    <UFormGroup label="Password" name="password">
      <UInput v-model="state.password" type="password" />
    </UFormGroup>

    <UButton type="submit">
      Login
    </UButton>
  </UForm>
</template>


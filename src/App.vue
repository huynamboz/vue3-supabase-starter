<script setup lang="ts">
import { onMounted, ref } from 'vue'
import Account from '@/pages/users/profile.vue'
import Auth from '@/pages/auth/login.vue'
import { supabase } from './supabase'

const session = ref()

onMounted(() => {
  supabase.auth.getSession().then(({ data }) => {
    session.value = data.session
  })

  supabase.auth.onAuthStateChange((_, _session) => {
    session.value = _session
  })
})
</script>

<template>
  <RouterView />
</template>
<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" required placeholder="display name" v-model="displayName">
    <input type="email" required placeholder="email" v-model="email">
    <input type="password" required placeholder="password" v-model="password">
    <button>Sign Up</button>
  </form>
  <div v-if="error" class="error">
    <p>{{ error }}</p>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import useSignup from '../composables/useSignup';

export default {
  setup(){
    const { error, signup } = useSignup();

    const displayName = ref('');
    const email = ref('');
    const password = ref('');

    const handleSubmit = async ( ) => {
      await signup(email.value, password.value, displayName.value);
      console.log('user signed up');
    }

    return { displayName, email, password, handleSubmit, error }
  }
}
</script>

<style>

</style>
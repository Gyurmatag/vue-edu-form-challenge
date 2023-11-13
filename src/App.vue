<template>
  <div
    class="min-h-screen bg-gray-100 flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8"
  >
    <div class="max-w-md w-full space-y-8">
      <div>
        <h2 class="mt-6 text-center text-3xl font-extrabold text-gray-900">
          Sign up for an account
        </h2>
      </div>
      <form class="mt-8 space-y-6" @submit.prevent="onSubmit">
        <div class="flex flex-col space-y-3 rounded-md shadow-sm -space-y-px">
          <div>
            <label
              for="email-address"
              class="block text-sm font-medium text-gray-700">
              Email address
            </label>
            <input
              id="email-address"
              name="email"
              type="email"
              autocomplete="email"
              required
              class="appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
              placeholder="Email address"
              v-model="form.email"
            />
            <p v-if="!isEmailValid" class="text-red-600">Email address is required</p>
          </div>
          <div>
            <label for="name" class="block text-sm font-medium text-gray-700">Full name</label>
            <input
              id="name"
              name="name"
              type="text"
              autocomplete="name"
              required
              class="appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
              placeholder="Full name"
              v-model="form.fullName"
            />
            <p v-if="!isFullNameValid" class="text-red-600">Full name should be between 5 and 250 characters</p>
          </div>
          <div>
            <label
              for="password"
              class="block text-sm font-medium text-gray-700">
              Password
            </label>
            <input
              id="password"
              name="password"
              type="password"
              autocomplete="new-password"
              required
              class="appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
              placeholder="Password"
              v-model="form.password"
            />
            <p v-if="!isPasswordValid" class="text-red-600">Password should be at least 8 characters</p>
          </div>
          <div>
            <label
              for="password-again"
              class="block text-sm font-medium text-gray-700">
              Password again
            </label>
            <input
              id="password-again"
              name="password-again"
              type="password"
              autocomplete="new-password"
              required
              class="appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
              placeholder="Password again"
              v-model="form.passwordAgain"
            />
            <p v-if="!isPasswordAgainValid" class="text-red-600">Password again is not equal to password</p>
          </div>
        </div>

        <div>
          <button
            type="submit"
            class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            :disabled="!isFormValid"
          >
            Sign Up
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { ref } from '@vue/reactivity';

let emailPattern = /^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/

let form = ref({
  email: '',
  fullName: '',
  password: '',
  passwordAgain: ''
})

let isEmailValid = computed(() => emailPattern.test(form.value.email))

let isFullNameValid = computed(() => {
  const fullNameLength = form.value.fullName.length
  return fullNameLength >= 5 && fullNameLength <= 250
})

let isPasswordValid = computed(() => form.value.password.length >= 8)

let isPasswordAgainValid = computed(() => form.value.passwordAgain.length >= 8 && form.value.password === form.value.passwordAgain)

let isFormValid = computed(() => {
  return isEmailValid.value && isFullNameValid.value && isPasswordValid.value && isPasswordAgainValid.value})

let onSubmit = () => {
  console.log(form.value)
}
</script>

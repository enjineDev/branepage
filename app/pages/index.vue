<script setup lang="ts">
import { useNotificationStore } from '../stores/notifications';

const notificationStore = useNotificationStore()

const contactData = ref({
  name: '',
  email: '',
  message: ''
})

const email = ref('')

const submitData = async (data) => {
  try {
    if (!data.email) {
      return notificationStore.addNotification({
        type: 'error',
        msg: 'Please provide any email address'
      })
    }
    if (!validEmail(data.email)) {
      return notificationStore.addNotification({
        type: 'error',
        msg: 'Not a valid e-mail-address!'
      })
    }
    await submitContact(data)
    notificationStore.addNotification({
      type: 'success',
      msg: 'Thanks! We will reply usally within the next 24h'
    })
  } catch (error) {
    notificationStore.addNotification({
      type: 'error',
      msg: error
    })
  }
}

const submitSubscription = async (data) => {
  try {
    if (!data) {
      return notificationStore.addNotification({
        type: 'error',
        msg: 'Please provide any email address'
      })
    }
    if (!validEmail(data)) {
      return notificationStore.addNotification({
        type: 'error',
        msg: 'Not a valid e-mail-address!'
      })
    }
    await subscribe(data)
    notificationStore.addNotification({
      type: 'success',
      msg: 'Thanks for subscribing'
    })
  } catch (error) {
    notificationStore.addNotification({
      type: 'error',
      msg: error
    })
  }
}

definePageMeta({
  layout: 'none'
})
</script>

<template>
  <div class="">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Blinker">

    <!-- Hero -->
    <section class="h-screen pt-24 overflow-hidden lg:pt-32 text-white">
      <div class="px-4 mx-auto max-w-7xl sm:px-6 lg:px-8">
        <div class="max-w-xl mx-auto text-center" data-aos="fade-down" data-aos-delay="100">
          <div class="mt-10 sm:mt-16" data-aos="fade-up" data-aos-delay="100">
            <img class="max-w-64 mx-auto -mb-16 rounded-full z-40" src="/logo.png" alt="" />
          </div>
          <div class="z-50 mt-16">
            <!-- <h2 class="text-5xl font-bold leading-tight lg:text-6xl">BRANE</h2> -->
            <p class="mt-4 leading-relaxed md:text-xl">Branding & Growth Hacking made easy.</p>
            <span>Launching soon Q2 2024</span>
          </div>
        </div>

        <div class="text-center pt-8">
          <p>BRANE Media is utilizing AI and Automations for Growth Hacks!</p>
        </div>

        <div class="flex flex-col items-center justify-center my-8">
            <h2>Subscribes, so you wont miss any Updates!</h2>
            <div class="flex pt-4">
              <input class="input bg-gray-900 placeholder:text-white" placeholder="E-Mail" type="email" v-model="email" @keyup.enter="submitSubscription(email)">
              <button class="btn btn-warning text-white" @click="submitSubscription(email)">Subscribe</button>
            </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style lang="css">
</style>

<template>
    <div class="container mx-auto flex bg-gray-500 my-4 rounded-full">
      <div>
        <img class="rounded-full h-12" :src="message.userPhotoURL" :alt="`Avatar of ${message.userName}`" />
      </div>
      <div class="flex flex-grow">
        <div class="flex flex-grow items-center justify-between mx-4 font-thin text-xl text-purple-200" :class="isUser ? 'bg-green-800' : 'bg-gray-700'">
          <p>{{ message.text }}</p>
          <p class="text-sm italic">{{ message.userName }}</p>
        </div>
      </div>
    </div>
  </template>

  <script setup>
    import { defineProps, computed, ref } from 'vue'
    import { authentication } from '~/helpers/useFirebase'

    const { user } = authentication()

    const isUser = computed(() => user.value.uid === props.message.userId)
    
    const props = defineProps({
      message: {
        type: Object,
        default: () => ({
          userName: '',
          userId: '',
          userPhotoURL: '',
          text: '',
          createdAt: '',
        }),
      },
    })
  </script>
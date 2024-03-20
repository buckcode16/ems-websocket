<template>
  Team

  <vue-advanced-chat
    :current-user-id="currentUserId"
    :rooms="JSON.stringify(rooms)"
    :messages="JSON.stringify(messages)"
    :messages-loaded="messagesLoaded"
    :room-actions="JSON.stringify(roomActions)"
    :rooms-loaded="true"
    @send-message="sendMessage($event.detail[0])"
    @fetch-messages="fetchMessages($event.detail[0])"
  />
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { register } from 'vue-advanced-chat'
register()

const currentUserId = ref('1234')
const rooms = ref([
  {
    roomId: '1',
    roomName: 'Room 1',
    avatar: 'https://66.media.tumblr.com/avatar_c6a8eae4303e_512.pnj',
    users: [
      { _id: '1234', username: 'John Doe' },
      { _id: '4321', username: 'John Snow' },
    ],
  },
])
const messages = ref([])
const messagesLoaded = ref(true)
const roomActions = ref([
  { name: 'inviteUser', title: 'Invite User' },
  { name: 'removeUser', title: 'Remove User' },
  { name: 'deleteRoom', title: 'Delete Room' },
])

const sendMessage = (message) => {
  messages.value = [
    ...messages.value,
    {
      _id: messages.value.length,
      content: message.content,
      senderId: currentUserId.value,
      timestamp: new Date().toString().substring(16, 21),
      date: new Date().toDateString(),
    },
  ]
}

const fetchMessages = () => {
  messagesLoaded.value = false
  messages.value = []
  setTimeout(() => {
    messagesLoaded.value = true
  })
}
</script>
<style scoped></style>

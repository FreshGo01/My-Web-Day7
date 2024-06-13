<script setup>
import { useLoginStore } from '../stores/login.js'
import { ref } from 'vue'
import http from '../services/http.js'

const loginStore = useLoginStore()
const uploadStatus = ref('')

async function uploadFile() {
  console.log(fileInput.value.files[0])
  const file = fileInput.value.files[0]
  if (!file) {
    uploadStatus.value = 'Please select a file.'
    return
  }
  uploadStatus.value = ''
  const formData = new FormData()
  formData.append('file', file)
  try {
    const res = await http.post('/auth/upload', formData, {
      headers: {
        'Content-Type': 'multipart/form-data'
      }
    })
    uploadStatus.value = res.data.message
    loginStore.updateLogin()
  } catch (error) {
    uploadStatus.value = error.response.data.message
  }
}
const fileInput = ref(null)

const image = ref('http://localhost:3000/uploads/' + loginStore.currentUser.image)
</script>
<template>
  <div>
    <img :src="image" alt="Profile image" style="width: 50px" />
  </div>
  <form @submit.prevent="uploadFile">
    <input type="file" ref="fileInput" /><span>{{ uploadStatus }}</span>
    <button type="submit">Upload</button>
  </form>
  <div>{{ loginStore.currentUser }} is login.</div>
</template>

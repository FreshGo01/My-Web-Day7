<script setup>
import { useLoginStore } from '../stores/login.js'

const loginStore = useLoginStore()

const image = loginStore.currentUser.image
  ? 'http://localhost:3000/uploads/' + loginStore.currentUser.image
  : 'http://localhost:3000/uploads/no-image.png'
</script>

<template>
  <div v-if="loginStore.isLogin()" class="profile-container">
    <div class="profile-image-wrapper">
      <img :src="image" alt="Profile image" class="profile-image" />
    </div>
    <div class="profile-info">
      <p class="profile-login">{{ loginStore.currentUser.login }} is logged in.</p>
      <button class="logout-button" @click="loginStore.logout">Logout</button>
    </div>
  </div>
</template>

<style scoped>
.profile-container {
  display: flex;
  align-items: center;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
  max-width: 300px;
  margin: 0 auto;
}

.profile-image-wrapper {
  margin-right: 10px;
}

.profile-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  object-fit: cover;
}

.profile-info {
  display: flex;
  flex-direction: column;
}

.profile-login {
  font-weight: bold;
  margin: 0 0 5px;
}

.logout-button {
  padding: 5px 10px;
  border: none;
  border-radius: 3px;
  background-color: #007bff;
  color: #fff;
  cursor: pointer;
}

.logout-button:hover {
  background-color: #0056b3;
}
</style>

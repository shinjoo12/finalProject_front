<template>
  <header>
    <div class="logo">
      <RouterLink to="/">
      전직시
      </RouterLink>
    </div>
    <nav class="menu">
      <RouterLink to="/certificate">자격증</RouterLink>
      <RouterLink to="/curation">채용</RouterLink>
      <RouterLink to="/board">자유게시판</RouterLink>
      <RouterLink to="/mypage">마이페이지</RouterLink>
      <RouterLink to="/login">로그인</RouterLink>
    </nav>
  </header>
</template>
  
<script setup>
import { RouterLink } from 'vue-router';
import '@/assets/css/header.css';
</script>

<style scoped>
</style>
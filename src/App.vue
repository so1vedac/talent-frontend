<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const videoData = ref({ title: '', url: '' })

onMounted(async () => {
  try {
    const res = await axios.get('http://localhost:8080/api/hero-video')
    videoData.value = res.data
  } catch (err) {
    console.error('서버 연결 실패:', err)
  }
})

const goPage = (pageName) => {
  alert(pageName + ' 페이지로 이동합니다 (준비중)')
}
</script>

<template>
  <div class="container">
    
    <header class="navbar">
      
      <div class="logo-area">
        <img src="/상징.jpg" alt="재능 로고" class="logo-img" />
      </div>

      <nav class="menu-area">
        
        <a href="#" @click.prevent="goPage('홈')" class="home-btn">홈</a>

        <div class="dropdown">
          <a href="#" class="dropbtn">자료실 ▾</a>
          <div class="dropdown-content">
            <a href="#" @click.prevent="goPage('알고리즘')">알고리즘</a>
            <a href="#" @click.prevent="goPage('정수론')">정수론</a>
            <a href="#" @click.prevent="goPage('게임 이론')">게임 이론</a>
          </div>
        </div>

        <a href="#" @click.prevent="goPage('재능 현황')">재능 현황</a>
        <a href="#" @click.prevent="goPage('재능 연혁')">재능 연혁</a>
        <a href="#" @click.prevent="goPage('재능 상징')">재능 상징</a>
        <a href="#" @click.prevent="goPage('게시판')">게시판</a>

      </nav>
    </header>

    <section class="hero-section">
      <video class="bg-video" autoplay muted loop playsinline v-if="videoData.url">
        <source :src="videoData.url" type="video/mp4" />
      </video>
      <div class="overlay"></div>
      
      <div class="content">
        <h1 class="title">SEX</h1>
        <p class="subtitle">너의 "재능"을 SEX로 증명하라</p>
      </div>
    </section>

  </div>
</template>

<style>
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');

body { margin: 0; padding: 0; font-family: 'Pretendard', sans-serif; background-color: #111; color: white; overflow-x: hidden; }

/* 네비게이션 바 */
.navbar {
  position: fixed; top: 0; left: 0; width: 100%; padding: 15px 40px;
  display: flex; justify-content: space-between; align-items: center;
  z-index: 1000;
  background: linear-gradient(to bottom, rgba(0,0,0,0.9), transparent);
}

/* 로고 스타일 (사진 크기 조절) */
.logo-img {
  height: 100px; /* 로고 높이 설정 (너무 크면 줄이세요) */
  width: auto;  /* 비율 유지 */
  cursor: pointer;
}

/* 메뉴 영역 */
.menu-area { display: flex; align-items: center; gap: 30px; }

.menu-area a {
  text-decoration: none; color: rgba(255, 255, 255, 0.8); font-size: 1rem; font-weight: 500; transition: color 0.3s;
}
.menu-area a:hover { color: white; }

/* 홈 버튼 스타일 */
.home-btn {
  background-color: white; color: black !important;
  padding: 8px 20px; border-radius: 20px; font-weight: bold;
}
.home-btn:hover { background-color: #ddd; }

/* 드롭다운 스타일 */
.dropdown { position: relative; display: inline-block; }
.dropdown-content {
  display: none; position: absolute; top: 30px; left: 50%; transform: translateX(-50%);
  background-color: rgba(0, 0, 0, 0.9); min-width: 120px;
  border-radius: 5px; padding: 10px 0;
}
.dropdown-content a { display: block; padding: 10px; text-align: center; }
.dropdown-content a:hover { background-color: #333; }
.dropdown:hover .dropdown-content { display: block; }

/* 히어로 섹션 */
.hero-section {
  position: relative; width: 100vw; height: 100vh;
  display: flex; justify-content: center; align-items: center;
}
.bg-video {
  position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);
  min-width: 100%; min-height: 100%; z-index: -2; object-fit: cover;
}
.overlay {
  position: absolute; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.5); z-index: -1;
}
.content { text-align: center; z-index: 1; }
.title { font-size: 6rem; font-weight: 900; letter-spacing: 10px; margin: 0; }
.subtitle { font-size: 1.5rem; margin-top: 20px; opacity: 0.9; }
</style>
<template>
    <div class="scrap-page">
      <h1 class="page-title"><i class="fas fa-bookmark"></i> 스크랩</h1>
      <div class="scrap-list">
        <div v-for="(item, index) in scrapItems" :key="index" class="scrap-item">
          <div class="scrap-content">
            <h3>{{ item.title }}</h3>
            <p>{{ item.company }}</p>
            <p>{{ item.location }}</p>
          </div>
          <div class="scrap-actions">
            <button @click="removeScrap(index)" class="remove-btn">
              <i class="fas fa-trash"></i>
            </button>
          </div>
        </div>
      </div>
      <div v-if="scrapItems.length === 0" class="empty-state">
        <i class="fas fa-folder-open"></i>
        <p>스크랩한 채용공고가 없습니다.</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ScrapPage',
    data() {
      return {
        scrapItems: [
          { title: '프론트엔드 개발자', company: '테크 솔루션즈', location: '서울 강남구' },
          { title: '백엔드 엔지니어', company: '클라우드 시스템즈', location: '경기 성남시' },
          { title: 'UI/UX 디자이너', company: '크리에이티브 랩', location: '서울 마포구' },
        ]
      }
    },
    methods: {
      removeScrap(index) {
        this.scrapItems.splice(index, 1);
      }
    }
  }
  </script>
  
  <style scoped>
  .scrap-page {
    padding: 20px;
  }
  
  .page-title {
    font-size: 28px;
    color: #333;
    margin-bottom: 30px;
  }
  
  .page-title i {
    color: #007bff;
    margin-right: 10px;
  }
  
  .scrap-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
  }
  
  .scrap-item {
    background: #ffffff;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: transform 0.3s ease;
  }
  
  .scrap-item:hover {
    transform: translateY(-5px);
  }
  
  .scrap-content h3 {
    font-size: 18px;
    color: #333;
    margin-bottom: 10px;
  }
  
  .scrap-content p {
    font-size: 14px;
    color: #666;
    margin: 5px 0;
  }
  
  .remove-btn {
    background: none;
    border: none;
    color: #dc3545;
    cursor: pointer;
    font-size: 18px;
    transition: color 0.3s ease;
  }
  
  .remove-btn:hover {
    color: #a71d2a;
  }
  
  .empty-state {
    text-align: center;
    padding: 50px 0;
    color: #666;
  }
  
  .empty-state i {
    font-size: 48px;
    margin-bottom: 20px;
    color: #007bff;
  }
  
  .empty-state p {
    font-size: 18px;
  }
  
  @media (max-width: 768px) {
    .scrap-list {
      grid-template-columns: 1fr;
    }
  }
  </style>
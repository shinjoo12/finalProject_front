<template>
  <div class="curationMaincontainer">
    <!-- 자격증 검색 -->
    <div class="selectcontainer">
      <div class="select">
        <p>보유하고 있는 자격증 또는 취득할 자격증을 선택하세요.</p>
      </div>
      <div class="input-group mb-3">
        <input type="text" v-model="certificate" class="form-control" placeholder="자격증의 이름을 입력하세요." aria-label="자격증" aria-describedby="button-addon2">
      </div>
      <div class="button-container">
        <button class="btn btn-outline-secondary" type="button" @click="onSelectComplete">선택 완료</button>
      </div>
    </div>
    <!-- 자격증 검색 끝 -->

    <!-- 그 외 큐레이션 부분 -->
    <div class="curationIndex">
      <div>
        <p>홈</p>
      </div>
      <div>
        <p>자격증</p>
      </div>
      <div>
        <p>지하철</p>
      </div>
      <div>
        <p>등등</p>
      </div>
    </div>
    
    <!-- 메인페이지 검색창 -->
    <div class="search-bar">
      <div class="cardinput">
        <input type="text" v-model="searchTerm" class="form-control" placeholder="채용 정보를 검색해보세요." aria-label="검색" aria-describedby="button-addon2">
        <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="searchJobs">검색</button>
      </div>
    </div>

    <!-- 채용정보 카드 -->
    <div class="recruitmentCards">
      <div class="row row-cols-1 row-cols-md-2 g-4">
        <div v-for="job in jobs" :key="job.jobId" class="col">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">{{ job.jobInfoTitle }}</h5>
              <p class="card-text">회사: {{ job.jobCompanyName }}</p>
              <p class="card-text">위치: {{ job.jobLocation }}</p>
              <p class="card-text">경력: {{ job.jobEmploymentType }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- 채용정보카드 끝 -->
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';

const router = useRouter();

// 상태 변수
const searchTerm = ref('');
const jobs = ref([]);

// 채용 정보를 가져오는 함수
const fetchJobs = async () => {
  try {
    const response = await axios.get('http://localhost:8090/api/jobinfo');  // 백엔드 URL
    // API 응답에서 필요한 데이터 추출
    const jobData = response.data.GetJobInfo.row;
    jobs.value = jobData.map(job => ({
      jobId: job.JO_REQST_NO,
      jobInfoTitle: job.JO_SJ,
      jobCompanyName: job.CMPNY_NM,
      jobLocation: job.WORK_PARAR_BASS_ADRES_CN,
      jobEmploymentType: job.EMPLYM_STLE_CMMN_CODE_SE
    }));
  } catch (error) {
    console.error('채용 정보를 가져오는 데 실패했습니다.', error);
  }
};

// 페이지가 로드될 때 채용 정보를 가져옴
onMounted(() => {
  fetchJobs();
});

// 검색 기능
const searchJobs = () => {
  // 검색 기능을 위한 로직 추가 필요
  console.log('검색어:', searchTerm.value);
};

// 카드를 클릭하면 CurationDetail 페이지로 이동
function goToDetail() {
  router.push({ name: 'curation-detail' });
}

// 자격증 선택 완료 핸들러
const onSelectComplete = () => {
  console.log('자격증 선택 완료:', certificate.value);
};

// 자격증 입력값
const certificate = ref('');
</script>

<style>

body {
  background-color: #E6F3FF;
}

/* 전체 컨테이너 레이아웃 */
.curationMaincontainer {
  font-family: Arial, sans-serif;
  margin: 0 auto;
  background-color: #ffffff;
  padding: 20px;
  box-sizing: border-box;
  width: 70%;
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 1px solid #ffffff;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
  position: relative;
}

/* 자격증 검색 큐레이션 css */
.selectcontainer {
  width: 100%;
  border: 1px solid #ddd;
  box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
  padding: 15px;
  margin-bottom: 20px;
}

.select p {
  margin-top: 10px;
  text-align: center;
}

.input-group {
  width: 100%;
}

.form-control {
  width: 100%;
  height: 6vh;
}

.button-container {
  display: flex;
  justify-content: flex-end;
  margin-top: 10px;
}

.btn {
  width: 150px; /* 너비를 더 넓히기 */
  height: 6vh;
  background-color: #0166FF;
  color: white;
}

.btn:hover {
  background-color: #002e83;
  color: white;
}

/* 검색창 스타일 */
.search-bar {
  display: flex;
  justify-content: flex-end;
  width: 100%;
  margin-bottom: 30px; /* 검색창 아래에 여유 공간 추가 */
}

.search-bar .cardinput {
  display: flex;
  align-items: center; /* input과 버튼을 수직으로 가운데 정렬 */
}

.search-bar input {
  height: 40px; 
  width: 300px;
  margin-right: 10px; /* 인풋창과 버튼 사이의 간격 추가 */
}

.search-bar .btn {
  height: 45px; 
  width: 80px;
}

/* 버튼 색상 및 호버 효과 */
.btn-outline-secondary {
  background-color: #007bff;
  color: white;
  border: none;
}

.btn-outline-secondary:hover {
  background-color: #0056b3;
  color: white;
  transition: background-color 0.3s;
}

/* 큐레이션 박스 스타일 */
.curationIndex {
  border: 1px solid #ddd;
  box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
  padding: 15px;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-around;
  width: 100%;
}

.curationIndex div {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* 채용정보 카드 스타일 */
.recruitmentCards {
  width: 100%;
  margin: 0 auto; /* 가운데 정렬 */
}

.recruitmentCards .row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.recruitmentCards .col {
  width: calc(50% - 10px);
  margin-bottom: 20px;
  display: flex;
}

.card {
  border: 1px solid #ddd;
  margin: 0px 10px;
  box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
  flex: 1;
  display: flex;
  flex-direction: column;
}

.card-body {
  padding: 15px;
  flex-grow: 1;
}



</style>

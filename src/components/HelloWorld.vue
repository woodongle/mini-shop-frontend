<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>{{ backendMessage }}</p>
    <button @click="fetchBackendMessage">백엔드 메시지 가져오기</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      backendMessage: '메시지를 기다리는 중...'
    };
  },
  methods: {
    async fetchBackendMessage() {
      try {
        // Spring Boot 백엔드 API 엔드포인트
        // CORS 설정을 확인하세요.
        const response = await axios.get('http://localhost:8080/api/hello');
        this.backendMessage = response.data;
      } catch (error) {
        console.error("백엔드 메시지를 가져오는 데 실패했습니다:", error);
        this.backendMessage = "오류 발생: 백엔드에 연결할 수 없습니다.";
      }
    }
  },
  mounted() {
    // 컴포넌트 마운트 시 자동으로 메시지를 가져오려면 아래 주석을 해제하세요.
    // this.fetchBackendMessage();
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
<template>
  <v-container>
    <v-row>
      <v-col
        v-for="book in books"
        :key="book.id"
        cols="12"
        md="4"
      >
        <v-card>
          <v-card-title>{{ book.title }} (ID: {{ book.id }})</v-card-title>
          <v-card-subtitle>{{ book.authorName }}</v-card-subtitle>
          <v-card-text>
            <p><strong>카테고리:</strong> {{ book.category }}</p>
            <p><strong>내용:</strong> {{ book.content }}</p>
            <p><strong>요약:</strong> {{ book.summaryContent }}</p>
            <p v-if="book.image"><strong>이미지 URL:</strong> <a :href="book.image" target="_blank">{{ book.image }}</a></p>
            <p v-if="book.pdfPath"><strong>PDF 경로:</strong> <a :href="book.pdfPath" target="_blank">{{ book.pdfPath }}</a></p>
            <p><strong>가격:</strong> {{ book.price }}</p>
            <p><strong>베스트셀러:</strong> {{ book.isBestSeller ? '예' : '아니오' }}</p>
            <p><strong>구독 수:</strong> {{ book.subscriptionCount }}</p>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'GetAllLibrary',
  data: () => ({
    books: [],
    headers: [
      { text: 'ID', value: 'id' },
      { text: '제목', value: 'title' },
      { text: '저자', value: 'authorName' },
      { text: '카테고리', value: 'category' },
      { text: '내용', value: 'content' },
      { text: '요약', value: 'summaryContent' },
      { text: '이미지', value: 'image' },
      { text: 'PDF', value: 'pdfPath' },
      { text: '가격', value: 'price' },
      { text: '베스트셀러', value: 'isBestSeller' },
      { text: '구독 수', value: 'subscriptionCount' },
    ],
  }),
  methods: {
    async search() {
      try {
        const response = await axios.get('/books')
        console.log('받은 데이터:', response.data) 
        this.books = response.data
      } catch (error) {
        console.error('도서 조회 실패:', error)
      }
    },
  },
  mounted() {
    this.search()
  }
}
</script>

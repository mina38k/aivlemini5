<!-- components/pages/SignUp.vue -->
<template>
  <v-container>
    <v-card>
      <v-toolbar color="primary" class="elevation-0 pa-4" height="50px">
        <div style="color:white; font-size:17px; font-weight:700;">회원가입</div>
      </v-toolbar>
      <v-card-text>
        <UserInfo
          :editMode="true"
          :isNew="true"
          :inList="false"
          :isSignUpMode="true"
          v-model="newUser"
          @add="registerUser"
        />
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
import UserInfo from '@/components/UserInfo.vue'
import axios from 'axios'
import BaseRepository from '@/components/repository/BaseRepository.js'  

export default {
  name: 'SignUp',
  components: { UserInfo },
  data() {
    return {
      newUser: {},
      repository: null,
    }
  },
  created() {
    // API baseURL과 path를 실제 환경에 맞게 설정
    this.repository = new BaseRepository(axios, 'userInfos')
  },
  methods: {
    async registerUser(user) {
      try {
        console.log('회원가입 요청:', user)

        // save(entity, isNew)에서 isNew=true로 새 데이터 생성 요청
        await this.repository.save(user, true)

        alert('회원가입이 완료되었습니다!')
        this.$router.push('/login') // 회원가입 후 로그인 페이지 이동
      } catch (e) {
        console.error('회원가입 실패', e)
        alert('회원가입에 실패했습니다. 다시 시도해주세요.')
      }
    }
  }
}
</script>

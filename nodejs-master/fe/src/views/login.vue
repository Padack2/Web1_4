<template>
  <v-container fill-height>
    <v-layout row wrap align-center>
      <v-flex xs12>
        <v-toolbar flat>
         <v-toolbar-title>로그인</v-toolbar-title>
       </v-toolbar>
        <v-card>
          <div class="pa-3">
            <v-text-field
                v-model="email"
                label="이메일을 입력하세요"

            >
            </v-text-field>
            <v-text-field
                v-model="password"
                label="패스워드를 입력하세요"
                type="password"
            >
            </v-text-field>
            <v-btn
             large
             block
             color="primary"
             @click="login()"
            >로그인</v-btn>
          </div>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      email: null,
      password: null,
      allUsers: [
        {id:1, name: 'genie', email:'genie@geniesoft.io', password:'12345'},
        {id:2, name: 'test', email:'test@geniesoft.io', password:'12345'}
      ]
    }
  },
  mounted () {
    axios.get('http://localhost:3000/api/signup')
        .then((r) => {
          this.allUsers = r.data.users
        })
        .catch((e) => {
          console.error(e.message)
        })
  },
  methods: {
    login() {
      let selectUser = null
      this.allUsers.forEach(user =>{
        if(user.email === this.email) selectUser = user
      })
        if (selectUser === null) {
        alert('입력하신 이메일이 없습니다')
        }  
        else{
        if(selectUser.password !== this.password){
          alert('이메일과 비밀번호가 일치하지 않습니다.')
        }
        else{
          alert('로그인 완료')
          location.replace("/")
        }
      }
      console.log(this.email, this.password)
    }
  }
}
</script>

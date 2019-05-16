<style scoped>
h1, h2 {
  font-weight: normal;
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

<template>
  <v-container fluid>
    <v-layout column align-center>
      <v-btn color="info" @click = "loginDialog()">Login</v-btn>
    </v-layout>
    <v-dialog v-model="dialog" persistent max-width="500px">
      <v-toolbar flat>
        <v-toolbar-title>로그인</v-toolbar-title>
          <v-btn fab dark small color="primary" style="left : 77%;" @click.native="dialog = false">
            <v-icon dark>remove</v-icon>
          </v-btn>
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
            <router-link to="/signup">
              <v-btn
                large
                block
                color="primary"
              >회원가입</v-btn>
            </router-link>
          </div>
        </v-card>
      </v-flex>
    </v-dialog>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      dialog: false,
      email: null,
      password: null,
      allUsers: [
        {id:1, name: 'genie', email:'genie@geniesoft.io', password:'12345'},
        {id:2, name: 'test', email:'test@geniesoft.io', password:'12345'}
      ]
    }
  },
  mounted () {
    this.dialog = false;
    axios.get('http://localhost:3000/api/signup')
        .then((r) => {
          this.allUsers = r.data.users
        })
        .catch((e) => {
          console.error(e.message)
        })
  },
  methods: {
    loginDialog () {
      console.log("loginddddd");
      this.dialog=true;
    },
    login() {
      // 전체 유저에서 해당 이메일로 유저를 찾는다.
      let selectUser = null
      this.allUsers.forEach(user =>{
        if(user.email === this.email) selectUser = user
      })
      if (selectUser === null) alert('입력하신 이메일이 없습니다')
        else{
        if(selectUser.password !== this.password)
          alert('이메일과 비밀번호가 일치하지 않습니다.')
          else{
          alert('로그인 완료')
          this.dialog = false
        }
      }
      // 그 유저의 비밀번호와 입력된 비밀번호를 비교한다.
      console.log(this.email, this.password)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

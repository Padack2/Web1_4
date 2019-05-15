<template>
<v-container fill-height>
  <v-layout row wrap align-center>
    <v-flex xs12>
      <v-toolbar flat>
        <v-toolbar-title>회원가입</v-toolbar-title>
      </v-toolbar>
      <v-card>
        <div class="pa-3">
          <v-text-field prepend-icon="star" v-model="email" label="이메일을 입력하세요">
          </v-text-field>
          <v-text-field prepend-icon="star" v-model="password" label="패스워드를 입력하세요" type="password">
          </v-text-field>
          <v-text-field v-model="name" label="이름을 입력하세요">
          </v-text-field>
          <v-text-field v-model="age" label="나이를 입력하세요">
          </v-text-field>
          <span>
            <i class="material-icons" display='inline'>star</i>
            <i>는 필수 입력항목입니다.</i>
          </span>

          <v-btn large block color="primary" @click="signup(password, email, name, age)">회원 가입</v-btn>
        </div>
      </v-card>
    </v-flex>
  </v-layout>
</v-container>
</template>

<script>
export default {
  data() {
    return {
      email: null,
      password: null,
      name: null,
      age: null,
    }
  },
  methods: {
    signup(password, email, name, age) {
      console.log(email, password, name, age);
      if (((password != '') && (password != null))&& ((email != '') && (email != null))) {
        if (!/^(?=.*[a-zA-Z])(?=.*[!@#$%^*+=-])(?=.*[0-9]).{8,25}$/.test(password)) {
          alert('비밀번호는 숫자+영문자+특수문자 조합으로 8자리 이상 사용해야 합니다.');
        } else {
          if (/(\w)\1\1\1/.test(password)) {
            alert('같은 문자를 4번 이상 사용하실 수 없습니다.');
          } else {
            alert('회원가입이 완료되었습니다.');
          }
        }
      } else {
        alert('아이디와 비밀번호를 입력해주세요');
      }
    }
  }
}
</script>

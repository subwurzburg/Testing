<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
        <VuetifyLogo />
      </v-card>
      <v-card>
        <v-card-text>
          <v-row>
            <v-col class="py-0" cols="12">
              <v-text-field
                v-model="username"
                label="請輸入帳號"
                :rules="[(v) => !!v || '請輸入帳號']"
                required
                filled
                dense
                autocomplete="username"
                :error-messages="errorMessages"
              ></v-text-field>
            </v-col>
            <v-col class="py-0" cols="12">
              <v-text-field
                v-model="password"
                :rules="[(v) => !!v || '請輸入密碼']"
                label="請輸入密碼"
                required
                filled
                dense
                type="password"
                :error-messages="errorMessages"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-row class="d-flex justify-center mx-10 my-10">
            <v-btn
              block
              large
              color="primary"
              type="submit"
              @click.prevent="login"
            >
              登入
            </v-btn>
          </v-row>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      username: '',
      password: '',
      errorMessages: '',
    }
  },
  mounted() {
    // 假如有token 未來需塞在Vuex(登入狀態)
    if (this.$cookies.get('token')) {
      this.$router.push('/questionnairePage')
      return
    }
  },
  methods: {
    login() {
      // 登入功能 (無api)
      if (this.canEntrance) {
        // 簡單設計一個token 未來會在Header內
        let token = Math.floor(new Date().getTime() / 1000)
        this.$cookies.set('token', token)
        this.$router.push('/questionnaire')
      } else {
        this.errorMessages = '帳號密碼錯誤'
      }
    },
  },
  computed: {
    // 無API驗證因此使用computed 驗證
    canEntrance() {
      return (
        this.username !== '' &&
        this.password !== '' &&
        this.username === 'test' &&
        this.password === 'test'
      )
    },
  },
}
</script>

<template>
  <v-row>
    <v-col cols="12" sm="8" md="12">
      <p>網站使用滿意度</p>
      <p>
        此問卷參考 John Brooke 所創建的 SUS 易用性量表，
        是目前被廣泛應用在快速測試產品系統界面、桌面程式與網站界面的標準化問卷（客觀性、普遍性、可重複、可量化）。
      </p>
      <p>詳細請參考 SurveyCake Blog 介紹</p>
      <ol>
        <li>請問你是第一次造訪我們網站嗎？</li>
        <div>
          <v-radio-group
            v-model="question1Selector"
            :row="!isMobile"
            hide-details
          >
            <div class="container d-flex fluid">
              <v-radio
                v-for="(n, index) in question[0].questionAns"
                :key="index"
                :label="`${n.title}`"
                :value="n.value"
              >
              </v-radio>
            </div>
          </v-radio-group>
        </div>
        <li>你是從哪些管道連到我們網站的呢？</li>
        <div class="container d-flex fluid flex-wrap">
          <v-checkbox
            v-for="(n, index) in question[1].questionAns"
            :key="index"
            v-model="question2Selector"
            :label="`${n.title}`"
            :value="n.value"
            required
          ></v-checkbox>
        </div>
      </ol>
    </v-col>
    <v-row class="d-flex justify-center mx-10 my-10">
      <v-btn block large color="primary" type="submit" @click.prevent="submit">
        確定
      </v-btn>
    </v-row>
  </v-row>
</template>

<style scoped>
.v-input--radio-group--column .v-radio:not(:last-child):not(:only-child) {
  margin: 0;
}
.v-radio,
.v-input {
  width: 50%;
}
.v-input__slot,
.v-input--selection-controls {
  margin: 0;
}
</style>
<script>
export default {
  name: 'QuestionnairePage',
  data() {
    return {
      question: [
        {
          questionAns: [
            {
              title: '是',
              value: true,
            },
            {
              title: '否',
              value: false,
            },
          ],
        },
        {
          questionAns: [
            {
              title: 'Goole 搜尋引擎',
              value: 0,
            },
            {
              title: 'Bing 搜尋引擎',
              value: 1,
            },
            {
              title: 'Facebook 粉絲專業',
              value: 2,
            },
            {
              title: 'Facebook 廣告推播',
              value: 3,
            },
            {
              title: 'Instagram 廣告推播',
              value: 4,
            },
            {
              title: '親友分享推薦',
              value: 5,
            },
            {
              title: '其他',
              value: 6,
            },
          ],
        },
      ],
      question1Selector: 'null', // 存放問題一的結果
      question2Selector: [], // 存放問題二的結果
    }
  },
  computed: {
    isMobile() {
      if (process.browser) {
        return window.innerHeight < 960
      }
    },
  },
  methods: {
    submit() {
      this.$cookies.remove('token')
      this.$router.push('/')
    },
  },
}
</script>

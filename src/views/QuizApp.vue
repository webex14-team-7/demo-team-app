<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ format.text }}</h2>
    <img
      class="quiz-image"
      :src="require(`@/assets/${format.quizes[quizNumber].image}.jpg`)"
      alt="お土産クイズ"
    />
    <div class="container">
      <button v-on:click="choiced(0)" v-if="buttonSeen">
        {{ format.quizes[quizNumber].choices[0].text }}
      </button>
      <button v-on:click="choiced(1)" v-if="buttonSeen">
        {{ format.quizes[quizNumber].choices[1].text }}
      </button>
      <button v-on:click="choiced(2)" v-if="buttonSeen">
        {{ format.quizes[quizNumber].choices[2].text }}
      </button>
    </div>
    <div>{{ feedback }}</div>
    <button v-if="seen" v-on:click="changeQuiz">次の問題へ</button>
    <div v-if="finish">これで問題は終わりだよ</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      feedback: "",
      quizNumber: 0,
      seen: false,
      buttonSeen: true,
      finish: false,
      format: {
        text: "このおみやげは何県の名物でしょう",
        quizes: [
          {
            image: "気になるリンゴ",
            choices: [
              {
                text: "青森県",
                isCorrect: true,
                feedback:
                  "正解！青森県の「気になるリンゴ」は中に丸ごと焼きりんごが入っているよ。",
              },
              {
                text: "沖縄県",
                isCorrect: false,
                feedback: "残念！沖縄県は元祖紅いもタルトが有名だね。",
              },
              {
                text: "埼玉県",
                isCorrect: false,
                feedback: "残念！埼玉県は十万石まんじゅうが有名だね。",
              },
            ],
          },
          {
            image: "桔梗信玄餅",
            choices: [
              {
                text: "福岡県",
                isCorrect: false,
                feedback: "残念！県は福岡は博多とおりもんが有名だね。",
              },
              {
                text: "北海道",
                isCorrect: false,
                feedback: "残念！北海道は白い恋人が有名だね。",
              },
              {
                text: "山梨県",
                isCorrect: true,
                feedback: "正解！山梨県は桔梗信玄餅が有名だよ。",
              },
            ],
          },
          {
            image: "赤い靴",
            choices: [
              {
                text: "神奈川県",
                isCorrect: true,
                feedback:
                  "正解！横浜を舞台にした童謡「赤い靴」をモチーフにしたチョコレート菓子だよ。",
              },
              {
                text: "広島県",
                isCorrect: false,
                feedback: "残念！広島県はもみじ饅頭がおいしいよね。",
              },
              {
                text: "奈良県",
                isCorrect: false,
                feedback: "残念！奈良県は柿の葉寿司が人気だよ",
              },
            ],
          },
          {
            image: "おやき",
            choices: [
              {
                text: "東京",
                isCorrect: false,
                feedback: "残念！東京は東京バナナでしょ！",
              },
              {
                text: "長野県",
                isCorrect: true,
                feedback: "正解！長野県のおやき、おいしそうだね！",
              },
              {
                text: "熊本県",
                isCorrect: false,
                feedback: "残念！くまもんが怒っちゃうよ💦",
              },
            ],
          },
        ],
      },
    }
  },
  methods: {
    choiced(i) {
      if (this.format.quizes[this.quizNumber].choices[i].isCorrect) {
        if (this.quizNumber <= 2) {
          this.seen = true
          this.buttonSeen = false
          this.feedback =
            this.format.quizes[this.quizNumber].choices[i].feedback
        } else {
          this.buttonSeen = false
          this.feedback =
            this.format.quizes[this.quizNumber].choices[i].feedback
          this.finish = true
        }
      } else {
        this.feedback = this.format.quizes[this.quizNumber].choices[i].feedback
      }
    },
    changeQuiz() {
      this.quizNumber += 1
      this.feedback = ""
      this.seen = false
      this.buttonSeen = true
    },
  },
}
</script>

<style>
.app {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.quiz-image {
  height: 300px;
  width: 300px;
  object-fit: contain;
}

.container {
  display: flex;
  height: 2em;
  width: 300px;
  padding: 1em;
  justify-content: space-around;
}
</style>

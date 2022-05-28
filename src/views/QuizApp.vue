<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ quiz.text }}</h2>
    <img
      class="quiz-image"
      src="@/assets/気になるリンゴ.jpg"
      alt="お土産クイズ"
    />
    <div class="container">
      <button v-on:click="choiced(0)">
        {{ format.quizes[quizNumber].choices[0].text }}
      </button>
      <button v-on:click="choiced(1)">
        {{ format.quizes[quizNumber].choices[1].text }}
      </button>
      <button v-on:click="choiced(2)">
        {{ format.quizes[quizNumber].choices[2].text }}
      </button>
    </div>
    <div>{{ feedback }}</div>
    <button v-if="seen">次の問題へ</button>>
  </div>
</template>

<script>
export default {
  data() {
    return {
      feedback: "",
      quizNumber: 0,
      seen: false,
      format: {
        text: "このおみやげは何県の名物でしょう",
        quizes: [
          {
            image: "気になるリンゴ.jpg",
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
            image: "桔梗信玄餅.jpg",
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
        ],
      },
    }
  },
  methods: {
    choiced(i) {
      this.seen = true
      this.feedback = this.format.quizes[this.quizNumber].choices[i].feedback
    },
    changeQuiz() {
      this.quizNumber += 1
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

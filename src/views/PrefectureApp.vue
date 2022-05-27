<template>
  <div>
    <h1>都道府県一覧をAPIで取得</h1>
    <div>
      <h2>都道府県一覧</h2>
      <button v-on:click="getQiitaArticle">都道府県と人口を取得する</button>
      <div v-for="(article, index) in articles" v-bind:key="index">
        {{ index }} :{{ article.localName }}: {{ article.population }}
      </div>
    </div>
    <div>
      <h2>QiitaのユーザーID</h2>
      <button v-on:click="getQiitaUser">ユーザーを取得する</button>
      <div>
        {{ user.id }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articles: [],
      user: {},
    }
  },
  methods: {
    getQiitaArticle: function () {
      const options = {
        method: "POST",
        headers: {
          "content-type": "application/json",
          "X-RapidAPI-Host": "list79.p.rapidapi.com",
          "X-RapidAPI-Key":
            "f8a01cb509msh7be0b80cead4a52p1c7e52jsnecd1010f659c",
        },
        body: '{"keyword":"","sort":"","currentPage":1,"itemsPerPage":100}',
      }
      fetch(
        "https://list79.p.rapidapi.com/country/8c7425bc-7d03-4b7d-95ac-ef35f02ee92e/regions",
        options
      )
        .then((res) => {
          return res.json() // res.json() は 文字列 -> JSのオブジェクトに変換する処理!
        })
        .then((value) => {
          console.log(value)
          this.articles = value.items
        })
        .catch((error) => {
          console.error(error)
        })
    },
    getQiitaUser: function () {
      fetch(`https://qiita.com/api/v2/authenticated_user`, {
        headers: {
          Authorization: "Bearer " + "アクセストークン",
        },
      })
        .then((res) => {
          return res.json()
        })
        .then((value) => {
          this.user = value
        })
    },
  },
}
</script>

<template>
  <div class="article-page">
    <div class="article-detail ">

    <h1 class="">Article</h1>
    <div class="blog-post">
      <div class="blog-content">
        <table class="blog-table">
          <tr>
            <th>제목</th>
            <td>{{ article.title }}</td>
          </tr>
          <tr>
            <th>내용</th>
            <td>{{ article.content }}</td>
          </tr>
          <tr>
            <th>작성자</th>
            <td class="author">{{ article.username }}</td>
          </tr>
        </table>
      </div>
    </div>
    <!-- <button class="submit-button" @click="updateComment(article)">수정하기</button> -->
    <hr />

    <h1>Comment</h1>
    <div class="comment-list">
      <div
        v-for="comment in commentList"
        :key="comment.id"
        class="comment-item"
      >
      <div class="d-flex justify-content-center ">

        <p class="comment-content" style="margin-right: 20px;">{{ comment.content }} </p>
        <p class="comment-user">작성자: {{ comment.user_username }}</p>
        <button class="delete-button" @click="deleteComment(comment.id)">
          DELETE
        </button>

      </div>
      </div>
    </div>
    <hr />

    <h1>Comment 작성하기</h1>
    <div class="comment-input" style="display: flex; justify-content: center">
      <!-- <label for="input-with-list">comment를 작성하세요</label> -->
      <b-form-input
        placeholder="Comment를 입력하세요."
        list="input-list"
        id="input-with-list"
        v-model="commentText"
        class="comment-input-field"
      ></b-form-input>
      <button class="submit-button" @click="sendComment()">Click</button>
    </div>
  </div>
  </div>
  
</template>

<script>
import axios from "axios";

export default {
  name: "ArticleDetail",
  data() {
    return {
      commentText: "",
      commentList: [],
    };
  },
  computed: {
    article() {
      return this.$store.state.articleDetail;
    },
    token() {
      return this.$store.state.token;
    },
  },
  created() {
    this.showComment();
  },
  methods: {
    showComment() {
      axios({
        method: "get",
        url: `http://127.0.0.1:8000/articles/${this.article.articlePk}/comment/create/`,
        headers: {
          Authorization: `Bearer ${this.token}`,
        },
      }).then((res) => {
        this.commentList = res.data;
      });
    },
    sendComment() {
      axios({
        method: "POST",
        url: `http://127.0.0.1:8000/articles/${this.article.articlePk}/comment/create/`,
        data: { content: this.commentText },
        headers: {
          Authorization: `Bearer ${this.token}`,
        },
      }).then((res) => {
        console.log(res);
        this.commentList = res.data;
        this.showComment();
        this.commentText = "";
      });
    },
    deleteComment(comment) {
      console.log("delete한다?", comment);
      axios({
        method: "delete",
        url: `http://127.0.0.1:8000/articles/${this.article.articlePk}/comment/delete/${comment}/`,
        headers: {
          Authorization: `Bearer ${this.token}`,
        },
      })
        .then(() => {
          console.log("삭제되었습니다.");
          this.showComment();
        })
        .catch((err) => {
          console.log(err);
        });
    },
    // updateComment(article) {
    //   console.log(article)
    //   axios({
    //     method: "put",
    //     url: `http://127.0.0.1:8000/articles/update/${this.article.articlePk}/`,
    //     data : {

    //     },
    //     headers: {
    //       Authorization: `Bearer ${this.token}`,
    //     },
    //   })
    //   .then(() => {
    //     console.log("수정되었습니다.");
    //     this.showComment();
    //   })
    //   .catch((err) => {
    //     console.log(err)
    //   })
    // }
  },
};
</script>

<style scoped>

.article-page {
  background: linear-gradient(to bottom, #C6426E, #642B73);
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.mt {
  margin-bottom:  30px;
}
.blog-post {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.blog-content {
  margin-bottom: 20px;
}

.blog-table {
  width: 100%;
  border-collapse: collapse;
}

.blog-table th {
  padding: 10px;
  text-align: left;
  background-color: #f2f2f2;
  font-weight: bold;
  border-bottom: 1px solid #ddd;
}

.blog-table td {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.blog-table .author {
  color: #007bff;
}

@media screen and (max-width: 480px) {
  .blog-table th,
  .blog-table td {
    display: block;
    width: 100%;
  }

  .blog-table th {
    margin-top: 10px;
    font-size: 14px;
  }
}
.comment-input-field {
  width: 300px;
}

.article-detail {
  margin: 20px;
}

h1 {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 10px;
}

p {
  margin-bottom: 5px;
}

.comment-list {
  margin-bottom: 10px;
}

.comment-item {
  margin-bottom: 5px;
  padding: 10px;
  background-color: #f2f2f2;
  border-radius: 5px;
}

.comment-content {
  margin: 0;
}
.comment-details {
  display: flex;
  align-items: center;
}
.comment-user {
  margin: 0;
  font-size: 12px;
}

.delete-button {
  margin-left: 10px;
  font-size: 12px;
  padding: 3px 6px;
  background-color: #ff8080;
  color: white;
  border: none;
  border-radius: 3px;
}

.comment-input {
  margin-bottom: 10px;
}

.submit-button {
  font-size: 14px;
  padding: 5px 10px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
}

.article-table {
  width: 100%;
  border-collapse: collapse;
}

.article-table th,
.article-table td {
  padding: 8px;
  border: 1px solid #ccc;
}

.article-table th {
  text-align: left;
  background-color: #f2f2f2;
}

.article-table td {
  word-break: break-word;
}

.author {
  font-size: 12px;
  color: #888;
}
</style>

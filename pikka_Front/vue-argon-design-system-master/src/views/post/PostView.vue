<template>
    <div class="post-view">
      <div class="logo-circle">
        <p>해당 게시글은 <br>추천상품을 <br>공유하는 게시판 입니다</p>
      </div>
      <h1 class="post-title">{{ post.title }}</h1>
      <div class="post-info">
        <span>작성자 : {{ post.writer }}</span>
        <span>작성일자 : {{ post.createdAt }}</span>
      </div>
      <div class="post-content" v-html="post.content"></div>
      <comment-section 
        :comments="post.comments"
        @add-comment="addComment"
      />
      <button @click="$emit('close')" class="btn btn-secondary mt-4">목록으로 돌아가기</button>
    </div>
  </template>
  
  <script>
  import CommentSection from './CommentSection.vue';
  
  export default {
    name: 'PostView',
    components: {
      CommentSection
    },
    props: ['post'],
    methods: {
      addComment(comment) {
        this.$emit('add-comment', comment);
      }
    }
  }
  </script>
  
  
  <style scoped>
  .write-post {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
  }
  .form-group {
    margin-bottom: 15px;
  }
  input, textarea {
    width: 100%;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  .form-actions {
    display: flex;
    justify-content: flex-end;
    gap: 10px;
  }
  .btn {
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  .btn-success {
    background-color: #28a745;
    color: white;
  }
  .btn-secondary {
    background-color: #6c757d;
    color: white;
  }
  </style>
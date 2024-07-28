<template>
    <div class="comments-section">
      <h3>댓글 {{ comments.length }}</h3>
      <div v-for="comment in comments" :key="comment.id" class="comment">
        <p>{{ comment.content }}</p>
      </div>
      <div class="comment-input">
        <input v-model="newComment" type="text" placeholder="댓글을 입력해주세요(최대 500자)" />
        <button @click="submitComment" :disabled="!newComment.trim()">
          <span class="circle"></span>
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CommentSection',
    props: {
      comments: {
        type: Array,
        default: () => []
      }
    },
    data() {
      return {
        newComment: ''
      }
    },
    methods: {
      submitComment() {
        if (this.newComment.trim()) {
          this.$emit('add-comment', this.newComment);
          this.newComment = '';
        }
      }
    }
  }
  </script>
  
  <style scoped>
  .comments-section {
    margin-top: 30px;
  }
  .comment {
    background-color: #f9f9f9;
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 5px;
  }
  .comment-input {
    display: flex;
    margin-top: 20px;
  }
  .comment-input input {
    flex-grow: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 20px;
    margin-right: 10px;
  }
  .comment-input button {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #4CAF50;
    border: none;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .comment-input button .circle {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: white;
  }
  </style>
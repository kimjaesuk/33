<template>
  <div class="write-post-container">
    <div class="write-post">
      <h2>게시글 작성</h2>
      <form @submit.prevent="submitPost">
        <div class="form-group">
          <input v-model="newPost.title" type="text" placeholder="제목" required>
        </div>
        <div class="form-group">
          <input v-model="newPost.writer" type="text" placeholder="작성자(mg)" required>
        </div>
        <div class="form-group">
          <textarea v-model="newPost.content" placeholder="내용을 입력하세요" rows="10" required></textarea>
        </div>
        <div class="form-actions">
          <button type="submit" class="btn btn-success">등록하기</button>
          <button type="button" @click="$emit('cancel')" class="btn btn-secondary">취소</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PostForm',
  data() {
    return {
      newPost: {
        title: '',
        writer: '',
        content: ''
      }
    }
  },
  methods: {
    submitPost() {
      this.$emit('submit-post', this.newPost);
      this.newPost = { title: '', writer: '', content: '' };
    }
  }
}
</script>

<style scoped>
.write-post-container {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 100vh;
  padding: 20px;
  box-sizing: border-box;
}
.write-post {
  width: 100%;
  max-width: 800px;
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
.form-group {
  margin-bottom: 15px;
}
input, textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
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
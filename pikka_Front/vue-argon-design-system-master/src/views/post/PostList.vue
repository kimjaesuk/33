<template>
    <div class="curation-board">
      <h1 class="text-center mb-4">취업 게시판</h1>
      
      <button @click="$emit('start-writing')" class="btn btn-primary mb-4">게시글 등록</button>
  
      <div class="grid">
        <div v-for="item in items" :key="item.id" class="card">
          <div class="card-image"></div>
          <div class="card-content">
            <h3 class="card-title">{{ item.title }}</h3>
            <p class="card-description">{{ item.description }}</p>
            <a @click.prevent="$emit('view-post', item.id)" href="#" class="card-link">자세히 보기</a>
          </div>
        </div>
      </div>
      <div class="pagination mt-4">
        <button 
          v-for="page in totalPages" 
          :key="page" 
          :class="{ active: currentPage === page }" 
          @click="$emit('set-page', page)"
        >
          {{ page }}
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'PostList',
    props: {
      items: Array,
      currentPage: Number,
      totalPages: Number
    }
  }
  </script>
  
  <style scoped>
  .curation-board {
    margin-top: 20px;
  }
  .grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 20px;
  }
  .card {
    background-color: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  }
  .card-image {
    width: 100%;
    height: 150px;
    background-color: #ddd;
  }
  .card-content {
    padding: 15px;
  }
  .card-title {
    color: #4a90e2;
    margin: 0 0 10px 0;
    font-size: 16px;
  }
  .card-description {
    font-size: 14px;
    color: #666;
    margin: 0 0 10px 0;
  }
  .card-link {
    color: #4a90e2;
    text-decoration: none;
    font-size: 14px;
  }
  .pagination {
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }
  .pagination button {
    margin: 0 5px;
    padding: 5px 10px;
    background-color: #fff;
    color: #4a90e2;
    border: 1px solid #4a90e2;
    border-radius: 4px;
    cursor: pointer;
  }
  .pagination button.active {
    background-color: #4a90e2;
    color: white;
  }
  .btn-primary {
    background-color: #4a90e2;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
  }
  </style>
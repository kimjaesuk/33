<template>
  <div class="profile-page">
    <section class="section-profile-cover section-shaped my-0">
      <div class="shape shape-style-1 shape-primary shape-skew alpha-4" style="background-image: linear-gradient(120deg, #a1c4fd 0%, #c2e9fb 100%);">
      </div>
    </section>
    <section class="section section-skew">
      <div class="container">
        <card shadow class="card-profile mt--300" no-body>
          <div class="px-4">
            <div class="row justify-content-center">
              <div class="col-lg-12 order-lg-3 text-lg-right align-self-lg-center">
                <div class="card-content">
                  <post-list 
                    v-if="!isWriting && !viewingPost" 
                    :items="displayedItems" 
                    :current-page="currentPage" 
                    :total-pages="totalPages"
                    @view-post="viewPost"
                    @set-page="setPage"
                    @start-writing="isWriting = true"
                  />
                  <post-form
                    v-if="isWriting"
                    @submit-post="submitPost"
                    @cancel="isWriting = false"
                  />
                  <post-view
                    v-if="viewingPost"
                    :post="currentPost"
                    @close="closePostView"
                    @add-comment="submitComment"
                  />
                </div>
              </div>
            </div>
          </div>
        </card>
      </div>
    </section>
  </div>
</template>
  
  <script>
  import PostList from './post/PostList.vue';
  import PostForm from './post/PostForm.vue';
  import PostView from './post/PostView.vue';
  
  export default {
    name: 'Profile',
    components: {
      PostList,
      PostForm,
      PostView
    },
    data() {
      return {
        isWriting: false,
        viewingPost: false,
        currentPage: 1,
        itemsPerPage: 16,
        items: [
          { 
            id: 1, 
            title: "추천 여행지", 
            description: "이번 시즌 꼭 가봐야 할 인기 여행지를 소개합니다.",
            content: "여행지에 대한 자세한 설명...",
            writer: "여행전문가",
            createdAt: "2023-05-15",
            comments: []
          },
          { 
            id: 2, 
            title: "맛집 리스트", 
            description: "현지인이 추천하는 숨은 맛집들을 모았습니다.",
            content: "맛집에 대한 자세한 설명...",
            writer: "맛집탐험가",
            createdAt: "2023-05-16",
            comments: []
          },
        ],
        currentPost: null,
        newPost: {
          title: '',
          writer: '',
          content: ''
        },
        newComment: ''
      };
    },
    computed: {
      totalPages() {
        return Math.ceil(this.items.length / this.itemsPerPage);
      },
      displayedItems() {
        const start = (this.currentPage - 1) * this.itemsPerPage;
        const end = start + this.itemsPerPage;
        return this.items.slice(start, end);
      }
    },
    methods: {
      setPage(page) {
        this.currentPage = page;
      },
      viewPost(id) {
        this.currentPost = this.items.find(item => item.id === id);
        this.viewingPost = true;
      },
      closePostView() {
        this.viewingPost = false;
        this.currentPost = null;
      },
      submitPost(newPost) {
        const newId = this.items.length + 1;
        this.items.unshift({
          id: newId,
          title: newPost.title,
          description: newPost.content.substring(0, 100) + '...',
          content: newPost.content,
          writer: newPost.writer,
          createdAt: new Date().toISOString().split('T')[0],
          comments: []
        });
        this.isWriting = false;
        this.currentPage = 1;
      },
      submitComment(comment) {
        if (!this.currentPost.comments) {
          this.$set(this.currentPost, 'comments', []);
        }
        this.currentPost.comments.push({
          id: Date.now(),
          content: comment,
          createdAt: new Date().toISOString()
        });
      }
    }
  };
  </script>
  
  <style scoped>
.profile-page {
  font-family: Arial, sans-serif;
}
.section-profile-cover {
  height: 200px;
  position: relative;
}
.section-skew {
  padding-top: 1.5rem;
  padding-bottom: 1.5rem;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
}
.card-profile {
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  margin-top: -150px;
  overflow: visible; /* changed from hidden */
}
.card-content {
  padding-top: 150px; /* Added to compensate for negative margin */
  min-height: calc(100vh - 200px); /* Ensures the card content takes up at least the full viewport height minus the cover section */
}
</style>
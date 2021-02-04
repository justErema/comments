<template>
   <div class="comment-list">
    <div class="comment-list__header">
      <h2>Продукт А</h2>
      <button class="btn btn-success">Сменить этап подбора</button>
    </div>
    <comment-input @add="addComment"></comment-input>
    <comment-card 
      v-for="comment in sortedComments"
      :key="comment.date" 
      :comment="comment"
      @edit="editComment"
      @delete="deleteComment">
    </comment-card>
  </div>
</template>

<script>
import CommentCard from '../../components/comments/CommentCard.vue';
import CommentInput from '../../components/comments/CommentInput.vue';

export default {
  name: 'comments',
  components: { CommentInput, CommentCard },

  data() {
    return {
      comments: []
    }
  },

  computed: {
    sortedComments() {
      const temp = [...this.comments];
      temp.sort((a,b) => 
        new Date(b.date) - new Date(a.date)
      );
      return temp;
    }
  },

  methods: {
    addComment(comment) {
      this.comments.push({ 
        text: comment,
        author: 'Вася Пупкин', 
        date: Date.now() 
      });
    },

    editComment(comment) {
      const index = this.comments.findIndex(item => item.date === comment.date);
      this.$set(this.comments, index, comment);
    },

    deleteComment(commentDate) {
      const index = this.comments.findIndex(item => item.date === commentDate);
      this.comments.splice(index, 1);
    },
  }
}
</script>

<style lang="scss">
  .comment-list {
    border-left: 2px solid #42b983;
    padding: 20px;
    &__header {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
  }
</style>
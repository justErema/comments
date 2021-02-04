<template>
  <div class="comment-card">
    <template v-if="!editMode">
      <h3 >{{ comment.text }}</h3>
      <div class="comment-card__info">
        <span>{{ comment.author }}, {{ formatedDate }} </span>
        <span class="arrow-bottom" @click.stop="showActionDialog = true"></span>
        <comment-action-dialog
          v-show="showActionDialog" 
          @delete="deleteComment()" 
          @edit="openEditMode()">
        </comment-action-dialog>
      </div>
    </template>
    <div v-else>
      <input ref="input" v-model="text">
      <button-group @confirm="editComment()" @cancel="closeEditMode()"></button-group>
    </div>
  </div>
</template>

<script>
import ButtonGroup from '../@common/ButtonGroup.vue'
import CommentActionDialog from './CommentActionDialog.vue'
export default {
  name: 'comment-card',

  props: ['comment'],

  components: { CommentActionDialog, ButtonGroup },

  data() {
    return {
      editMode: false,
      showActionDialog: false,
      text: this.comment.text
    }
  },

  computed: {
    formatedDate () {
      const date = new Date(this.comment.date);
      const monthNames = [
        'Января',
        'Февраля',
        'Марта',
        'Апреля',
        'Мая',
        'Июня',
        'Июля',
        'Августа',
        'Сентября',
        'Ноября',
        'Декабря',
      ];

      return `${date.getDate()} ${monthNames[date.getMonth()]}`;
    }
  },

  methods: {
    deleteComment() {
      this.$emit('delete', this.comment.date);
    },

    editComment() {
      this.$emit('edit', { 
        ...this.comment,
        text: this.text,
      });
      this.editMode = false;
    },

    openEditMode() {
      this.editMode = true;
      this.$nextTick(() => {
        this.$refs["input"].focus();
      });
    },

    closeEditMode() {
      this.editMode = false;
      this.text = this.comment.text;
    }
  },

  mounted () {
    document.body.addEventListener('click', () => {
      this.showActionDialog = false;
    });
  }
}
</script>

<style lang="scss">
  .comment-card {
    text-align: left;
    & > h3 {
      margin-bottom: 5px;
    }
    &__info {
      position: relative;
      display: inline-flex;
      align-items: center;
      & > span {
        text-transform: uppercase;
        color: #ccc;
      }
      .arrow-bottom {
        cursor: pointer;
        width: 0; 
        height: 0; 
        border-left: 10px solid transparent;
        border-right: 10px solid transparent;
        
        border-top: 10px solid #ccc;
        margin-left: 10px;
      }
    }
    & input {
      outline: none !important;
      border: none;
      width: 100%;
      padding: 5px 0;
      color: #212121;
      font-weight: bold;
      font-size: 18px;
    }
    margin-bottom: 20px;
    
  }
</style>


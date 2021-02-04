<template>
  <div class="add-comment">
    <input 
      ref="input"
      v-model="comment"
      type="text" 
      placeholder="Написать комментарий" 
      @focus="focus = true" 
      @blur="focus = false"
    >
    <button-group 
      v-show="focus || !!comment" 
      @confirm="addComment()" 
      @cancel="clearInput()">
    </button-group>
  </div>
</template>

<script>
import ButtonGroup from '../@common/ButtonGroup.vue';
export default {
  name: 'comment-input',
  
  components: { ButtonGroup },

  data() {
    return {
      focus: false,
      comment: ""
    }
  },

  methods: {
    addComment() {
      this.$emit('add', this.comment);
      this.clearInput();
    },

    clearInput() {
      this.comment = "";
      this.$refs["input"].blur();
    }
  }
}
</script>

<style lang="scss" scoped>
  .add-comment {
    border-top: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
    padding: 10px 0;
    margin-bottom: 40px;
    & > input {
      outline: none !important;
      border: none;
      width: 100%;
      padding: 5px 0;
      color: #212121;
      font-weight: bold;
      font-size: 18px;
    }
    & > .action-buttons {
      margin-top: 20px;
    }
  }
</style>
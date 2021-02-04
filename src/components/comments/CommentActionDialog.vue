<template>
  <div class="action-dialog" @click.stop="">
    <div class="action-dialog__delete-confirm" v-if="showDeleteConfirm">
      <p>Вы точно хотите удалить комментарий?</p>
      <button-group 
        :confirmText="'Удалить'" 
        :confirmStyle="'danger'" 
        @confirm="$emit('delete')" 
        @cancel="showDeleteConfirm = false">
      </button-group>
    </div>
    <template v-else>
      <a @click.prevent="$emit('edit')">Редактировать</a>
      <a @click.prevent="showDeleteConfirm = true">Удалить</a>
    </template>
  </div>
</template>

<script>
import ButtonGroup from '../@common/ButtonGroup.vue';

export default {
  name: 'comment-action-dialog',

  components: { ButtonGroup },

  data() {
    return {
      showDeleteConfirm: false
    }
  }
}
</script>

<style lang="scss" scoped>
  .action-dialog {
    position: absolute;
    top: 100%;
    left: 100%;
    background: white;
    border: 1px solid #212121;
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
    border-radius: 8px;
    &__delete-confirm {
      min-width: 300px;
      padding: 20px 10px;
      display: flex;
      flex-direction: column;
    }
    & > a {
      cursor: pointer;
      display: block;
      padding: 10px 30px;
      text-align: left;
      color: #212121;
      text-transform: none;
      &:hover {
        opacity: .8;
      }
      &:not(:last-child) {
        border-bottom: 1px solid #000;
      }
    }
  }
</style>
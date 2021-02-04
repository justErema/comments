<template>
   <div class="action-buttons">
      <button :class="`btn btn-${confirmStyle}`" @click="$emit('confirm')">{{confirmText}}</button>
      <button class="btn btn-default" @click="$emit('cancel')">{{cancelText}}</button>
    </div>
</template>

<script>
export default {
  name: 'button-group',

  props: {
    confirmText: {
      type: String,
      default: 'Сохранить'
    },
    confirmStyle: {
      type: String,
      default: 'primary'
    },
    cancelText: {
      type: String,
      default: 'Отмена'
    }
  },
  
}
</script>
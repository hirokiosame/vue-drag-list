<template>
  <div
    class="divider"
    :class="{ hover }"
    @dragover.prevent
    @dragenter="dragEnter"
    @dragleave="dragLeave"
    @drop.stop="itemDrop"
  />
</template>

<script>
export default {
  name: 'DragListDivider',

  inject: {
    draglist: 'draglist',
  },

  data() {
    return {
      hover: false,
    }
  },

  methods: {
    dragEnter() {
      this.hover = true;
    },
    dragLeave() {
      this.hover = false;
    },
    itemDrop() {
      this.hover = false;
      this.$emit('item-dropped', this.draglist.draggedItem);
    }
  }
}
</script>

<style scoped>
.divider {
  width: 100%;
  height: 3px;
  padding: 2px 0;
  background-clip: content-box;

  &.hover {
    background-color: blue;
  }
}
</style>
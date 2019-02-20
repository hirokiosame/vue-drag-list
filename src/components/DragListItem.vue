<template>
  <li
    class="item"
    :class="{ dragging }"
    v-show="!invisible"
    :draggable="dragEnabled"
    @dragstart="dragStart"
    @dragend="dragEnd"
  >
    <div
      class="dragHandle"
      :class="{ dragging }"
      @mouseover="enableDrag"
      @mouseleave="disableDrag"
    >
      ::
    </div>
    <slot />
  </li>
</template>

<script>
export default {
  name: 'DragList',

  props: {
    item: null,
  },

  inject: {
    draglist: 'draglist',
  },

  data() {
    return {
      dragEnabled: false,
      dragging: false,
      invisible: false,
    };
  },

  methods: {
    enableDrag() {
      this.dragEnabled = true;
    },
    disableDrag() {
      this.dragEnabled = false;
    },
    dragStart() {
      this.dragging = true;
      this.draglist.draggedItem = this.item;
      setTimeout(() => {
        this.invisible = true;
      }, 0);
    },

    dragEnd() {
      this.draglist.draggedItem = null;
      this.dragging = false;
      this.invisible = false;
    },
  }
}
</script>

<style scoped>
.item {
  border: 1px solid #ccc;
  text-align: left;
}

.dragHandle {
  display: inline-block;
  background-color: #ccc;
  width: 10px;
  height: 100%;
  cursor: grab;

  &.dragging {
    cursor: grabbing;
  }
}

</style>
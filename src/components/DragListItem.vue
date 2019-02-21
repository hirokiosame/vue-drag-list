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

    {{ item.label }}

    <template v-if="item.children">
      <drag-list
        class="childList"
        v-show="!dragging"
        :parent-idx="idxPath"
        :listData="item.children"
      />
    </template>
  </li>
</template>

<script>
export default {
  name: 'DragListItem',

  props: {
    parentArr: Array,
    item: null,
    idxPath: Array,
  },

  components: {
    DragList: () => import('./DragList'),
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
    dragStart(e) {
      e.stopPropagation();
      this.dragging = true;

      Object.assign(this.draglist, {
        draggedFromPath: this.idxPath,
        draggedItem: this.item,
      });

      setTimeout(() => {
        this.invisible = true;
      }, 0);
    },

    dragEnd() {
      Object.assign(this.draglist, {
        draggedFromPath: null,
        draggedItem: null,
      });

      Object.assign(this, {
        dragging: false,
        invisible: false,
      });
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
  height: 100%;
  cursor: grab;
  padding: 2px 4px;

  &.dragging {
    cursor: grabbing;
  }
}

.childList {
  margin-left: 16px;
}

</style>
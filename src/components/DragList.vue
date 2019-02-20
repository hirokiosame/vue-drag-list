<template>
  <ul class="list">
    <drag-list-divider @item-dropped="moveItem($event, 0)" />
    <template v-for="(item, idx) in listData">
      <drag-list-item
        :key="`item${idx}`"
        :item="item"
      >
        {{ item.label }}
      </drag-list-item>
      <drag-list-divider
        :key="`divide${idx}`"
        v-show="item !== state.draggedItem"
        @item-dropped="moveItem($event, idx + 1)"
      />
    </template>
  </ul>
</template>

<script>
import DragListItem from './DragListItem';
import DragListDivider from './DragListDivider';

export default {
  name: 'DragList',

  props: {
    listData: {
      type: Array,
    }
  },

  components: {
    DragListItem,
    DragListDivider,
  },

  data() {
    return {
      state: {
        draggedItem: null
      },
    };
  },

  provide() {
    return {
      draglist: this.state,
    };
  },

  methods: {
    moveItem(item, moveToIdx) {
      const removeIdx = this.listData.indexOf(item);
      this.listData.splice(removeIdx, 1);

      if (removeIdx < moveToIdx) {
        moveToIdx -= 1;
      }
      this.listData.splice(moveToIdx, 0, item);
    },
  },
};
</script>

<style scoped>

.list {
  border: 1px solid #ccc;
  list-style-type: none;
  padding: 0;
}

</style>
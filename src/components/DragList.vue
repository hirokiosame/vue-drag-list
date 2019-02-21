<template>
  <ul class="list">
    <drag-list-divider @item-dropped="moveItem($event, getPath(0))" />
    <template v-for="(item, idx) in listData">
      <drag-list-item
        :key="`item${idx}`"
        :idx-path="getPath(idx)"
        :item="item"
        :parentArr="listData"
      />
      <drag-list-divider
        :key="`divide${idx}`"
        v-show="item !== state.draggedItem"
        @item-dropped="moveItem($event, getPath(idx + 1))"
      />
    </template>
  </ul>
</template>

<script>
import DragListItem from './DragListItem';
import DragListDivider from './DragListDivider';

const findParentByPath = (arr, pathArr) => {
  let node = arr;

  for (let i = 0; i < pathArr.length - 1; i++) {
    const idx = pathArr[i];
    node = node[idx];   

    if (!Array.isArray(node)) {
      node = node.children;
    } 
  }

  return node;
};

export default {
  name: 'DragList',

  props: {
    listData: {
      type: Array,
    },
    parentIdx: {
      type: Array,
      default: () => [],
    },
  },

  components: {
    DragListItem,
    DragListDivider,
  },

  inject: {
    draglist: {
      from: 'draglist',
      default: undefined,
    },
  },

  data() {
    return {
      state: this.draglist || {
        draglistRoot: this.listData,
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
    getPath(idx) {
      return this.parentIdx.concat([idx]);
    },
    moveItem(item, toPath) {
      const fromPath = this.state.draggedFromPath;
      const fromParent = findParentByPath(this.state.draglistRoot, fromPath);
      const toParent = findParentByPath(this.state.draglistRoot, toPath);
      const fromIdx = fromPath.slice(-1)[0];
      let toIdx = toPath.slice(-1)[0];

      if (fromParent === toParent && fromIdx < toIdx) {
        toIdx -= 1;
      }

      fromParent.splice(fromIdx, 1);
      toParent.splice(toIdx, 0, item);
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
<template>
  <div
    :id="id"
    :class="classNames.join(' ')"
    :draggable="isDraggable"
    :style="'width: '+ (width) +'em; height: '+ (height) + 'em;'"
  ></div>
</template>

<script>
export default {
  props: {
    isDraggable: {
      type: Boolean,
      default: true
    },
    data: {
      type: Array,
      default: undefined
    },
    id: {
      type: String,
      default: ""
    },
    classNames: {
      type: Array,
      default() {
        return ["draggable"];
      }
    },
    width: {
      type: Number,
      default: 17.5
    },
    height: {
      type: Number,
      default: 17.5
    }
  }
};
</script>

<style>
.draggable {
  border: rgb(64, 109, 22) solid 1px;
  height: 17.5em;
  width: 17.5em;
  background-color: rgb(123, 255, 0);
}
</style>

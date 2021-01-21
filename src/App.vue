<template>
  <div id="app">
    <h2>Drag and Drop with Vue</h2>

    <div class="container">
      <div class="row">
        <div class="flex flex-center">
          <drop-zone :id="dropZoneId"></drop-zone>
        </div>
      </div>
    </div>
    <div class="container">
      <div @dragstart="onDragStart($event)" @dragend="onDragEnd($event)">
        <draggable :id="draggableId"></draggable>
      </div>
    </div>
    <div class="container" v-if="showButton">
      <div class="row">
        <div class="flex flex-center">
          <button @click="reset">Reset</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DropZone from "./components/drop/DropZone.vue";
import Draggable from "./components/drag/Draggable.vue";

export default {
  name: "App",
  components: {
    DropZone,
    Draggable
  },

  data() {
    return {
      draggableId: "draggable",
      dropZoneId: "drop-zone",
      showButton: false
    };
  },

  methods: {
    onDragStart(event) {
      const target = event.target;

      if (target) {
        event.dropEffect = "move";
        event.dataTransfer.setData("text/plain", target.id);
        event.target.style.opacity = 0.4;
      }
    },

    onDragEnd(event) {
      if (event.target) {
        event.target.style.opacity = "";
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  height: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.row {
  display: flex;
  margin-bottom: 8em;
}

.flex {
  flex: 0 0 auto;
}

.flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* media queries */
@media screen and (max-width: 48em) {
  .container {
    flex-direction: column;
  }
}
</style>

<template>
  <div
    :id="id"
    :class="classNames.join(' ')"
    @drop="onDrop($event)"
    @dragenter="onDragEnter($event)"
    @dragleave="onDragLeave($event)"
    @dragover="onDragOver($event)"
  >
    <span class="dashing">
      <i></i>
    </span>
    <span class="dashing">
      <i></i>
    </span>
    <span class="dashing">
      <i></i>
    </span>
    <span class="dashing">
      <i></i>
    </span>
    <slot />
  </div>
</template>

<script>
export default {
  components: {},
  props: {
    classNames: {
      type: Array,
      default() {
        return ["drop-zone"];
      }
    },
    id: {
      type: String,
      default: ""
    },
    isDropZone: {
      type: Boolean,
      default: true
    },
    width: {
      type: Number,
      default: 1
    }
  },
  data() {
    return {};
  },

  methods: {
    validateTarget(target) {
      const dropZone = document.getElementById(this.id);
      return target.parentNode === dropZone || target === dropZone
        ? dropZone
        : null;
    },

    contains(list, value) {
      for (let i = 0; i < list.length; ++i) {
        if (list[i] === value) {
          return true;
        }
      }
      return false;
    },

    canBeCharged(ligne_commande) {
      if (ligne_commande) {
        return true;
      }
      return false;
    },

    onDragOver(event) {
      event.preventDefault();
    },

    onDragLeave(event) {
      event.target.style.background = "";
    },

    onDragEnter(event) {
      const target = this.validateTarget(event.target);

      if (this.isDropZone) {
        if (target) {
          if (event.target) {
            event.preventDefault();
            event.dataTransfer.dropEffect = "move";
            event.target.style.backgroundColor = "#25c467";
          } else {
            event.target.style.background = "#f13e3e";
          }
        } else {
          event.target.style.background = "#f13e3e";
        }
      } else {
        event.target.style.background = "#f13e3e";
      }
    },

    onDrop(event) {
      if (this.isDropZone) {
        event.target.style.backgroundColor = "";

        const target = this.validateTarget(event.target);

        if (target) {
          if (event.target) {
            event.preventDefault();
            var data = event.dataTransfer.getData("text/plain");
            var dragged = document.getElementById(data);
            dragged.style.opacity = 1;
            event.target.appendChild(dragged);
          }
        }
      }
    }
  }
};
</script>

<style>
.drop-zone {
  /* position: relative; */
  width: 18em;
  height: 18em;
  overflow: hidden;
  background: #878787;
  color: white;
  box-shadow: 0 19px 38px rgba(0, 0, 0, 0.3), 0 15px 12px rgba(0, 0, 0, 0.22);
  display: flex;
  align-items: center;
  justify-content: center;
  border: dashed 5px;
}
</style>

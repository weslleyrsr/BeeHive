<template>
  <section id="container" @mousedown="mouseDownHandler" class="bee-hive">
    <slot></slot>
  </section>
</template>

<script>
export default /*#__PURE__*/{
  name: 'BeeHive', // vue component name
  data() {
    return {
      pos: {}
    };
  },
  computed: {
    "element": function () {
      return document.getElementById('container');
    }
  },
  methods: {
    mouseMoveHandler: function (e) {
      // How far the mouse has been moved
      const dx = e.clientX - this.pos.x;
      const dy = e.clientY - this.pos.y;

      // Scroll the element
      this.element.scrollTop = this.pos.top - dy;
      this.element.scrollLeft = this.pos.left - dx;
    },
    mouseDownHandler: function (e) {
      // Change the cursor and prevent user from selecting the text
      this.element.style.cursor = 'grabbing';
      this.element.style.userSelect = 'none';

      this.pos = {
        // The current scroll
        left: this.element.scrollLeft,
        top: this.element.scrollTop,
        // Get the current mouse position
        x: e.clientX,
        y: e.clientY,
      };

      document.addEventListener('mousemove', this.mouseMoveHandler);
      document.addEventListener('mouseup', this.mouseUpHandler);
    },
    mouseUpHandler: function () {
      document.removeEventListener('mousemove', this.mouseMoveHandler);
      document.removeEventListener('mouseup', this.mouseUpHandler);

      this.element.style.cursor = 'grab';
      this.element.style.removeProperty('user-select');
    }
  },
};
</script>

<style lang="scss">
$hexagon-width: 150px;
$hexagon-height: calc($hexagon-width*.55);

.bee-hive {
  display: grid;
  width: 100%;
  height: 100%;
  padding: 16px;
  cursor: grab;
  overflow: auto;
}
</style>
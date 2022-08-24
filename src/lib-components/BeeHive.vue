<template>
  <section class="bee-hive">
    <slot></slot>
  </section>
</template>

<script>
export default /*#__PURE__*/{
  name: 'BeeHive', // vue component name
  data() {
    return {};
  },
  computed: {},
  methods: {},
};
</script>

<style lang="scss">
$hexagon-width: 150px;
$hexagon-height: calc($hexagon-width*.55);

.bee-hive {
  display: grid;
  width: 100%;
  height: 100%;
  overflow: auto;
}
</style>
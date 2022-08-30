<template>
    <div
        id="hexagon"
        ref="hexagon"
        :class="`hexagon ${active && 'active'}`"
        :style="`--color: ${color || '#0043CE'};`"
        @mousedown="emitSelected"
    >
        <slot></slot>
    </div>
</template>

<script>
export default {
  name: 'BeeHiveItem', // vue component name
  props: {
    "item": { "type": Object, "required": true },
    "color": { "type": String, "default": "#0043CE", "required": false },
    "active": { "type": Boolean, "default": false, "required": false},
  },
  data() {
    return {
        initialMousePosition: {},
        currentMousePosition: {}
    }
  },
  computed: {},
  methods: {
    emitSelected: function(e) {
        this.initialMousePosition.x = e.clientX;
        this.initialMousePosition.y = e.clientY;

        this.currentMousePosition.x = e.clientX;
        this.currentMousePosition.y = e.clientY;

        document.addEventListener("mousemove", (e) => {
            this.currentMousePosition.x = e.clientX;
            this.currentMousePosition.y = e.clientY;
        });

        setTimeout(() => {
            if (this.currentMousePosition.x === this.initialMousePosition.x && this.currentMousePosition.y === this.initialMousePosition.y) {
                this.$emit("select", this.item);
            }
        }, 50);
    }
  },
};
</script>

<style lang="scss">
$hexagon-width: 150px;
$hexagon-height: $hexagon-width*.55;
$hexagon-margin: 8px;
$hexagon-title-color: #fff;
$hexagon-border-color: #fff;

*,
*::before,
*::after {
    box-sizing: border-box;
}

.active {
    opacity: 0.6;
}

.hexagon {
    flex: 0 0 $hexagon-width;
    width: $hexagon-width;
    height: $hexagon-height;
    margin: calc($hexagon-height/2) calc($hexagon-margin/4);
    position: relative;
    padding: 0.5em;
    cursor: pointer;

    text-align: center;
    z-index: 1;

    &__title {
        // height: 100%;
        // display: flex;
        width: 100%;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        flex-direction: column;
        justify-content: center;
        hyphens: auto;
        word-break: break-word;
        text-transform: uppercase;
        color: #fff;
        font-weight: 700;
        font-size: 1em;
        transition: opacity 350ms;
        text-overflow: ellipsis;

        // Remove this in the future
        // max-height: 30px;

        >small {
            font-weight: 300;
            margin-top: 0.25em;
        }
    }

    // &::before,
    &::after {
        content: '';
    }

    // &::before,
    &::after,
    &__image {
        top: -50%;
        left: 0;
        width: 100%;
        height: 200%;
        display: block;
        position: absolute;
        clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
        z-index: -1;
    }

    // &::before {
    //     background: $hexagon-border-color;
    //     transform: scale(1.055);
    // }

    &::after {
        background: var(--color);
        opacity: 1;
        transition: opacity 350ms;
    }

    &:hover {

        .honeycomb-cell__title {
            opacity: 0;
        }

        // &::before {
        //     background: var(--hover-color);
        // }

        &::after {
            opacity: 0.5;
            // background: var(--hover-color);
        }
    }
}
</style>
<template>
    <div :class="getClasses()" :data-label="label">
        <slot></slot>
    </div>
</template>

<script>
export default /*#__PURE__*/{
    name: 'BeeHiveRow', // vue component name
    props: {
        index: { type: Number, required: true },
        children: { type: Number, required: true },
        rowBefore: { type: Number, required: false },
        label: { type: String, required: true }
    },
    computed: {
        even() {
            return this.index % 2 == 0;
        },

        childrenEven() {
            return this.children % 2 == 0;
        },

        rowBeforeEvenIndex() {
            return this.index > 0 ? (this.index - 1) % 2 == 0 : true
        },

        rowBeforeEvenChildren() {
            return this.rowBefore ? this.rowBefore % 2 == 0 : true
        },

        needOffset() {
            if (this.even && !this.childrenEven) {
                return true
            }

            if (!this.even && this.childrenEven) {
                return true
            }

            if (!this.even && this.childrenEven && this.rowBeforeEvenIndex && this.rowBeforeEvenChildren) {
                return true
            }

            return false
        },
    },
    methods: {
        getClasses() {
            let classes = "row"

            // if (this.even) {
            //     classes += ' row-even'
            // } else {
            //     classes += ' row-odd'
            // }

            if (this.needOffset) {
                classes += ' offset'
            }

            return classes;
        }
    },
    onUpdate: function () {
        console.log({
            "even": even.value,
            "childrenEven": childrenEven.value,
            "rowBeforeEvenIndex": rowBeforeEvenIndex.value,
            "rowBeforeEvenChildren": rowBeforeEvenChildren.value
        })
    }
};
</script>

<style lang="scss" scoped>
    $hexagon-width: 150px;
    $hexagon-height: $hexagon-width*.55;

    .row {
        display: flex;
        // justify-content: center; 
    }

    .row:not(:first-child) {
        margin-top: calc(0px - ($hexagon-height/2.2));
    }

    .offset {
        padding-left: $hexagon-width/2 + 2;
    }
</style>
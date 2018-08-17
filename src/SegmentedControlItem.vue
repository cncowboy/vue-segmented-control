<template>
    <div class="segmented-item" :style="theItemStyle"
        @click="onSelect">
        {{ option[label] }}
    </div>
</template>

<script>
export default {
    name: 'SegmentedControlItem',
    props: {
        option: {
            type: Object,
            required: true
        },
        label: {
            type: String,
            default: 'label'
        },
        value: {
            type: String,
            default: 'value'
        },
        color: {
            type: String,
            default: '#fff'
        },
        activeColor: {
            type: String,
            default: '#000'
        },
        optionsSelected: {
            type: Array,
            default: []
        }
    },
    data () {
        return {
        }
    },
    mounted () {
        console.log('option', this.option)
    },
    computed: {
        segmentedControlStyle: function () {
            return `color: ${this.activeColor}; border: solid 1px ${this.activeColor}`
        },
        theItemStyle: function () {
            if (this.valuesSelected.includes(this.option[this.value])) {
                return this.itemSelectedStyle
            } else {
                return this.itemStyle
            }
        },
        itemStyle: function () {
            return `borderRight: solid 1px ${this.activeColor};is-selected: false;`
        },
        itemSelectedStyle: function () {
            return `color: ${this.color}; background: ${this.activeColor};is-selected: true;`
        },
        valuesSelected: function () {
            return this.optionsSelected.map(option => option[this.value])
        }
    },
    methods: {
        onSelect () {
            this.$emit('select', this.option)
        }
    }
}
</script>

<style>
    .segmented-item {
        flex: 1;
        padding: 10px;
        transition: all .3s ease;
        text-align: center;
        user-select: none;
    }

    .segmented-item:last-child {
        border: none!important;
    }

    .is-selected {
        color: white;
    }
</style>

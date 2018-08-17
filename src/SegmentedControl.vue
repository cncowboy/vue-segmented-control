<template>
    <div class="segmented-control" :style="segmentedControlStyle">
        <segmented-control-item 
            v-for="(option, key) in options" 
            :option="option" 
            :label="label"
            :value="value"
            :color="color"
            :activeColor="activeColor"
            :optionsSelected="optionsSelected"
            @select="onSelect" :key="option" />
    </div>
</template>

<script>
import SegmentedControlItem from './SegmentedControlItem'

export default {
    components: {
        SegmentedControlItem
    },
    props: {
        options: {
            type: Array,
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
        multiple: {
            type: Boolean,
            default: false
        }
    },
    data () {
        return {
            optionsSelected: []
        }
    },
    computed: {
        segmentedControlStyle: function () {
            return `color: ${this.activeColor}; border: solid 1px ${this.activeColor}`
        },
        valuesSelected: function () {
            return this.optionsSelected.map(option => option[this.value])
        }
    },
    methods: {
        onSelect (option) {
            if (this.multiple === true) {
                if (this.optionsSelected.find(optionSelected => optionSelected.value === option.value)) {
                    this.optionsSelected = this.optionsSelected.filter(optionSelected => optionSelected.value !== option.value)
                } else {
                    this.optionsSelected.push(option)
                }
            } else {
                this.optionsSelected = [option]
            }

            console.log('SegmentedControl, select:', this.optionsSelected)
            this.$emit('select', this.optionsSelected)
        }
    }
}
</script>

<style>
    .segmented-control {
        display: flex;
        flex-direction: row;
        border-radius: 5px;
    }
</style>

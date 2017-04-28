<template>
    <div class="m-radio" @change="$emit('change', currentValue)">
        <div class="radio-tt" v-text="title"></div>
        <div v-for="option in options">
            <label class="radio-label">
                <span class="radio-label-r">
                    <input
                        class="radio-label-input"
                        type="radio"
                        v-model="currentValue"
                        :disabled="option.disabled"
                        :value="option.value || option"
                    >
                </span>
                <span class="radio-label-t" v-text="option.label || option"></span>
            </label>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Radio',
    props: {
        title: String,
        align: String,
        options: {
            type: Array,
            required: true
        },
        value: String
    },
    data() {
        return {
            currentValue: this.value
        };
    },
    watch: {
        value(val) {
            this.currentValue = val;
        },
        currentValue(val) {
            this.$emit('input', val);
        }
    },
};
</script>

<style lang="scss">

</style>

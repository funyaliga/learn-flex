<template>
<div id="app">
    <div class="flex-container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
    <div class="radio flex-direction">
        <Radio :options="f.flexDirection.options" @change="flexDirectionChange($event)"></Radio>
        <div v-for="item in f.flexDirection.options">
            {{ item }}
        </div>
    </div>
</div>
</template>

<script>
import Radio from './components/radio.vue';
export default {
    name: 'app',
    components: {
        [Radio.name]: Radio,
    },
    data () {
        return {
            f: {
                flexDirection: {
                    selected: 'row',
                    options: ['row', 'row-reverse', 'column', 'column-reverse']
                }
            },
            test: '测试',
        }
    },
    methods: {
        flexDirectionChange(val) {
            console.log(val)
            // this.f.flexDirection.selected = val
            // console.log(this.f.flexDirection)
        },
    },
}
</script>

<style lang="scss">
    @import "./assets/main.scss";
</style>

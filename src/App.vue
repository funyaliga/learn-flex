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
        <div v-for="item in f.flexDirection.options">
            {{ item }}
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'app',
    data () {
        return {
            f: {
                flexDirection: {
                    selected: 'row',
                    options: ['row', 'row-reverse', 'column', 'column-reverse']
                }
            }
        }
    }
}
</script>

<style lang="scss">
    @import "./assets/main.scss";
</style>

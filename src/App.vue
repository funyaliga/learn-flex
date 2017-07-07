<template>
<div id="app">
    <div class="m-view">
        <div class="box" :style="styleBox">
            <div v-for="i in 5" :key="i" class="item" :style="styleItem[i]"><p>{{ i }}</p></div>
        </div>
    </div>

    <div class="m-ctr">
        <div v-for="(v, styleName) in f" :key="v.title" class="floor">
            <!-- radio -->
            <div v-if="v.type === 'radio'" :class="`z-${v.type}`">
                <h3>{{v.title}}</h3>
                <c-radio :options="v.options" :defaultValue="v.selected" @change="radioChange($event, styleName)"></c-radio>
            </div>

            <div v-else-if="v.type === 'child'" :class="`z-${v.type}`">
                <h3>{{v.title}} <em v-if="v.subtitle">({{v.subtitle}})</em></h3>
                <c-select v-for="i in 5" :key="`select-${i}`"  :label="i" :options="v.options" :defaultValue="v.selected[i - 1]" @change="childChange($event, styleName, i)" ></c-select>
            </div>
        </div>
    </div>

    <div class="m-intro">

    </div>

</div>
</template>

<script>
import cRadio from './components/radio.vue';
import cSelect from './components/select.vue';
export default {
    name: 'app',
    components: {
        [cRadio.name]: cRadio,
        [cSelect.name]: cSelect,
    },
    data () {
        return {
            f: {
                flexDirection: {
                    title: 'flex-direction',
                    type: 'radio',
                    selected: 'row',
                    options: ['row', 'row-reverse', 'column', 'column-reverse'],
                },
                flexWrap: {
                    title: 'flex-wrap',
                    type: 'radio',
                    selected: 'nowrap',
                    options: ['nowrap', 'wrap', 'wrap-reverse'],
                },
                justifyContent: {
                    title: 'justify-content',
                    type: 'radio',
                    selected: 'flex-start',
                    options: ['flex-start', 'center', 'flex-end', 'space-between', 'space-around'],
                },
                alignContent: {
                    title: 'align-content',
                    type: 'radio',
                    selected: 'stretch',
                    options: ['flex-start', 'center', 'flex-end', 'space-between', 'space-around', 'stretch'],
                },
                alignItems: {
                    title: 'align-items',
                    type: 'radio',
                    selected: 'stretch',
                    options: ['flex-start', 'center', 'flex-end', 'baseline', 'stretch'],
                },
                alignSelf: {
                    title: 'align-self',
                    type: 'child',
                    selected: ['auto', 'auto', 'auto', 'auto', 'auto'],
                    options: ['auto', 'flex-start', 'flex-end', 'center', 'baseline', 'stretch'],
                },
                flexGrow: {
                    title: 'flex-grow',
                    subtitle: '拉伸比率',
                    type: 'child',
                    selected: ['0', '0', '0', '0', '0'],
                    options: ['0', '1', '2', '3'],
                },
                flexShrink: {
                    title: 'flex-shrink',
                    subtitle: '收缩比率',
                    type: 'child',
                    selected: ['1', '1', '1', '1', '1'],
                    options: ['0', '1', '3', '5'],
                },
                flexBasis: {
                    title: 'flex-basis',
                    subtitle: '元素宽度',
                    type: 'child',
                    selected: ['auto', 'auto', 'auto', 'auto', 'auto'],
                    options: ['auto', '10%', '30%', '50%'],
                },
                order: {
                    title: 'order',
                    subtitle: '排列顺序',
                    type: 'child',
                    selected: ['0', '0', '0', '0', '0'],
                    options: ['-2', '-1', '0', '1', '2'],
                },
            },
            test: '测试',
            itemsLen: {}, //元素长度
            styleBox: {}, // 盒子样式
            styleItem: {}, // 子元素样式
            focus: '',
        }
    },
    created () {
        const styleBox = {}
        const styleItem = {}
        for (const i in [...Array(5)]) {
            styleItem[+i + 1] = {}
        }
        for (const key in this.f) {
            if (this.f.hasOwnProperty(key)) {
                const element = this.f[key];
                if (element.type === 'radio') {
                    styleBox[key] = element.selected
                } else {
                    for (const i in [...Array(5)]) {
                        styleItem[+i + 1][key] = element.selected
                    }
                }
            }
        }
        this.styleBox = styleBox
        this.styleItem = styleItem
    },
    methods: {
        radioChange(val, styleName) {
            this.f[styleName].selected = val
            this.styleBox[styleName] = val
            this.focus = styleName
        },
        childChange(val, styleName, i) {
            // 克隆一个object
            const styleItem = Object.assign({}, this.styleItem)
            if(!styleItem[i]) {
                styleItem[i] = {}
            }
            styleItem[i][styleName] = val

            this.f[styleName].selected.splice(i - 1, 1, val)
            this.styleItem = styleItem
            this.focus = styleName
        },
    },
}
</script>

<style lang="scss">
    @import "./assets/main.scss";
</style>

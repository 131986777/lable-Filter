<template>
    <div class="land">
        <div class="filter-wrap" style="width:1200px;">
            <div class="filter-main-wrap">
                <div class="filter-main">
                    <plug-filter @name="getName" :screenList="screenList"></plug-filter>
                    <plug-lable :dynamicTags="dynamicTags" @tag="getTag"></plug-lable>

                </div>
            </div>
        </div>
    </div>
</template>

<script type="text/ecmascript-6">
    import plugFilter from './plugFilter'
    import plugLable from './plugLable'
    import './filter.css'

    export default {
        props: ['screenList'],
        data() {
            return {
                dynamicTags: []
            }
        },
        created() {
        },
        methods: {
            getName(name) {
                this.dynamicTags = name
                this.$emit('msg', name)
            },
            getTag(tag, dynamicTags) {
                //操作 plugFilter
                this.screenList.forEach(item => {
                    item.shopList.forEach(items => {
                        if (items.name == tag) {
                            items.active = false

                        }
                    })
                })
                this.$emit('msg', dynamicTags)
            }
        },

        components: {
            plugFilter,
            plugLable
        }
    }
    ;
</script>

<style>
    /*注释独立样式*/

</style>

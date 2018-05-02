<template>
    <div>
        <div class="screen filter-list clearfix open" v-for=" (screenList,index) in screenList ">
            <label class="filter-name c-383838 w60 mt6 ml20">{{screenList.title+':'}}</label>
            <div class="filter-value-wrap">
                <ul class="filter-value clearfix mt6">
                    <li :class="[screenList.active?'active':'']" @click="cgAllFilter(index, screenList)"
                        class="filter-item w60 all">
                        {{screenList.allName}}
                    </li>
                    <li v-for="item in screenList.shopList"
                        :class="[item.active==true && screenList.active==false?'active':'']"
                        @click="cgFilter(item, screenList)"
                        class="filter-item w60">
                        {{item.name}}
                    </li>
                </ul>
            </div>
        </div>
    </div>


</template>

<script>
    export default {
        name: "shop",
        props: ['screenList'],
        data() {
            return {
                active: true,
                item: '',
                Index: '',
                result: [],

            }
        },
        methods: {
            cgFilter(item, screenList) {
                screenList.active = false;
                item.active = !item.active;
                this.pushResult()

            },
            cgAllFilter(index, item) {
                // //重置
                item.active = true;
                item.shopList.forEach(item => {
                    item.active = false;
                })
                this.pushResult()

            },
            pushResult() {
                //传出结果
                this.result = [];
                this.screenList.forEach(item => {
                    item.shopList.forEach(items => {
                        if (items.active) {
                            this.result.push(items.name)
                        }
                    })
                })
                this.$emit('name', this.result)
            }
        },
        watch: {
            screenList: {
                //监听 当没有选中时默认选中第一个
                deep: true,
                handler: function () {
                    this.screenList.forEach(screenListItem => {
                        var itemActiveCount = 0;
                        screenListItem.shopList.forEach(item => {
                            if (item.active) {
                                itemActiveCount++;
                            }
                        })
                        if (itemActiveCount <= 0) {
                            screenListItem.active = true;
                        } else {
                            screenListItem.active = false;
                        }
                    })
                }

            }
        },
        mounted() {
            this.screenList.forEach(item => {
                item.active = true;
            })

        }
    }
</script>

<style scoped lang="scss">
    .active {
        font-weight: bold;
        color: #00B355;

    }

    /*.screen {*/
    /*!*fonf-size:14px*!*/
    /*padding: 6px;*/
    /*margin: 14px 0;*/
    /*overflow: hidden;*/
    /*height: 50px;*/
    /*width: 84%;*/

    /*}*/

    /*label {*/
    /*float: left;*/
    /*margin-left: 10px;*/
    /*width: 50px;*/
    /*}*/

    /*ul {*/
    /*float: left;*/
    /*overflow: hidden;*/
    /*position: relative;*/
    /*text-align: center;*/
    /*padding-left: 50px;*/

    li {
        /*float: left;*/
        /*width: 60px;*/
        cursor: pointer;

    }

    /*}*/

    /*.active {*/
    /*color: red;*/
    /*}*/

</style>

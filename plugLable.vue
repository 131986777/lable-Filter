<template>
    <div class="lable">
        <div>所选分类</div>
        <div>
            <el-tag
                :key="tag"
                v-for="tag in dynamicTags"
                closable
                :disable-transitions="false"
                @close="handleClose(tag)">
                {{tag}}
            </el-tag>
        </div>
    </div>
</template>

<script>
    export default {
        name: "plug-lable",
        data() {
            return {
                inputVisible: false,
                inputValue: ''
            };
        },
        props: ['dynamicTags'],
        methods: {
            handleClose(tag) {

                this.dynamicTags.splice(this.dynamicTags.indexOf(tag), 1);
                this.$emit('tag', tag, this.dynamicTags)
            },

        }
    }
</script>

<style scoped lang="scss">
    .el-tag + .el-tag {
        margin-left: 10px;
    }

    .lable {
        height: 40px;
        line-height: 40px;

        div {
            display: inline-block;
            padding-left: 20px;
        }
    }
</style>

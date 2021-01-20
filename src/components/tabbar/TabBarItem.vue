<template>
    <div class="tab-bar-item" @click="tabbarClick">
        <!-- 两张图片的插槽 
        外面包层div防止插槽的某些属性被替换掉-->
        <div v-if="!isActive"><slot name="item-icon"></slot></div>
        <div v-else> <slot name="item-icon-active"></slot></div>
        <!-- 文本的插槽，用style属性动态获取样式 -->
        <div :style="activeStyle"><slot name="item-text"></slot></div>
    </div>
</template>

<script>
export default {
    name: 'TabBarItem',
     props: {
        path: String,
        activeColor: {
            type: String,
            default: "red"
        }
    },
    data() {
        return {
            // isActive: true
        }
    }, 
   
    // 通过this.$route.path获取到活跃的路径，用indexOf方法进行判断
    computed: {
        isActive() {
           return this.$route.path.indexOf(this.path) !== -1
        },
        activeStyle() {
            // 用this.isActive判断是否处于活跃状态，处于活跃返回样式对象，否则返回空对象。
            return this.isActive ? {color: this.activeColor} : {}
        }
    },
    methods: {
        tabbarClick() {
           // 路由跳转
           this.$router.replace(this.path)
        }
    }
}
</script>

<style scoped>
 .tab-bar-item{
     flex: 1;
     text-align: center;
     height: 49px;
     font-size: 14px;
 }

 .tab-bar-item img{
     width: 24px;
     height: 24px;
     margin-top: 3px;
     vertical-align: middle;
     margin-bottom: 2px;
 }

 .active{
     color: palevioletred;
 }
</style>
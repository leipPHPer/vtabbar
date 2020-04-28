<template>
    <div class="tab-bar-item" @click="itemClick">
        <slot v-if="!isActive" name="item-icon"></slot>
        <slot v-else name="item-icon-active"></slot>
        <!--<div :class="{active:isActive}">-->
        <!--    <slot name="item-text"></slot>-->
        <!--</div>-->
        <div :style="isActiveColor">
            <slot name="item-text"></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: "TabBarItem",
        props: {
            path: String,
            activeColor: {
                type: String,
                default: 'red'
            }
        },
        data() {
            return {
                // isActive: false,
            }
        },
        computed: {
            isActive() {
                return this.$route.path.indexOf(this.path) !== -1
            },
            isActiveColor() {
                return this.isActive ? {color:this.activeColor} : {}
            }
        },
        methods: {
            itemClick() {
                this.$router.replace(this.path)
            }
        }
    }
</script>

<style scoped>
    .tab-bar-item{
        flex             :1;
        text-align       :center;
        height           :49px;
        background-color :#f6f6f6;
    }
    .tab-bar-item img {
        width :24px;
    }
    .active {
        color :red;
    }
</style>
<template>
    <transition name="moveR">
        <div v-show="showFlag" class="food">
            <div class="food-content">
                <div class="image-header">
                    <img :src="food.image" alt="">
                    <div class="back" @click="hide">
                        <i class="icon-arrow_lift"></i>
                    </div>
                </div>
                <div class="content">
                    <h1 class="title">{{food.name}}</h1>
                    <div class="detil">
                        <span class="sell-count">月售:{{food.sellCount}}份</span>
                        <span class="rating">好拼率:{{food.rating}}</span>
                    </div>
                    <div class="price">
                        <span class="now">￥{{food.price}}</span>
                        <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        props:{
            food:{
                type:Object
            }
        },
        data() {
            return {
                showFlag: false
            }
        },
        methods:{
            show(){
                this.showFlag = true
            },
            hide(){
                this.showFlag = false
            },
        }
    }
</script>

<style lang="stylus" scoped rel="stylesheet/stylus">
    .food
        position fixed;
        top:0
        left:0
        bottom:48px
        z-index:30;
        width:100%;
        background :#fff;
        &.moveR-enter-active,  .moveR-leave-active 
            transition: all 0.2s linear;
            transform: translateX(0);
        &.moveR-enter,  .moveR-leave 
            transform: translateX(100%);
        &.moveR-leave-to
            transform: translateX(100%);
        .image-header
            position relative
            width:100%
            height:0
            padding-top:100%
            img
                position absolute
                top:0
                left:0
                width:100%
                height:100%
            .back
                position absolute
                top:10px
                left:0
                .icon-arrow_lift
                    display :block
                    font-size:20px;
                    color :#fff;
                    padding:10px;

</style>
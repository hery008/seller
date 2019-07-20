<template>
    <div class="goods">
        <div class="meau-wrapper" ref="meauWrapper">
            <ul>
                <li v-for="(item,index) in goods" :key="index" class="meau-item">
                    <span class="text border-1px">
                        <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span> {{item.name}}    
                    </span>    
                </li> 
            </ul>
        </div>
        <div class="foods-wrapper" ref="foodWrapper">
            <ul>
                <li v-for="(item,index) in goods" :key="index" class="foods-list food-list-hook">
                    <h1 class="title">{{item.name}}</h1>
                    <ul>
                        <li v-for="(food,indexs) in item.foods" :key="indexs" class="food-item border-item">
                            <div class="icon">
                                <img width="57" heigh="57" :src="food.icon">
                            </div>
                            <div class="content">
                                <h2 class="name">{{food.name}}</h2>
                                <p class="desc">{{food.description}}</p>
                                 <div class="extra">
                                    <span class="count">月售{{food.sellCount}}份</span>
                                    <span>好评率{{food.rating}}</span>
                                </div>
                                <div class="price">
                                    <span class="now">￥{{food.price}}</span>
                                    <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                                </div>
                            </div>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>          
    </div>
</template>

<script>
    import axios from 'axios'
    import BScroll from 'better-scroll'
    export default {
        props:{
            seller:{
                type:Object
            }
        },
        data() {
            return {
                goods: [],
                classMap : ['decrease','discount','special','invoice','guarantee'],
                listHeight: [],
                scrollY:0
            }
        },
        created(){
             axios.get('../static/data.json')
            .then(res=>{
                this.goods = res.data.goods
                this.$nextTick(()=>{
                    this._initScroll()
                    this._calculateHeight()
                })
            })
            .catch(err=>{
                console.log(err)
            })
        },
        methods:{
            _initScroll(){
                this.meauScroll = new BScroll(this.$refs.meauWrapper,{})
                this.foodScroll = new BScroll(this.$refs.foodWrapper,{
                    probeType:3
                })
                this.foodScroll.on('scroll',(pos)=>{
                    this.scrollY = Math.abs(Math.round(pos.y))
                })
            },
            _calculateHeight(){
                let foodList = this.$refs.foodWrapper.getElementsByClassName("food-list-hook")
                let height = 0
                this.listHeight.push(height)
                for(let i = 0; i<foodList.length; i++){
                    let item = foodList[i]
                    height += item.clientHeight
                    this.listHeight.push(height)
                }
            }
        }
    }
</script>

<style lang="stylus" scoped rel="stylesheet/stylus">
@import "../../common/stylus/mixin"
.goods
    display:flex
    position:absolute
    top:174px;
    bottom:46px;
    width :100%;
    overflow :hidden
    .meau-wrapper
        flex:0 0 80px;
        width:80px;
        background-color :#f3f5f7;
        .meau-item
            display :table;
            padding:0 12px;
            width:56px;
            height:54px;
            line-height:14px;
            .icon
                display:inline-block
                vertical-align :top
                width:12px
                height 12px
                margin-right:2px
                background-size:12px 12px
                background-repeat :no-repeat
                &.decrease
                    bg-image('decrease_3')
                &.discount
                    bg-image('discount_3')
                &.guarantee
                    bg-image('guarantee_3')
                &.invoice
                    bg-image('invoice_3')
                &.special
                    bg-image('special_3')
            .text
                display :table-cell;
                width:56px;
                vertical-align :middle;
                font-size:12px;
                border-1px(rgba(7,17,27,0.1))
    .foods-wrapper
        flex:1; 
        .title
            padding-left:14px;
            height:26px;
            line-height :26px;
            border-left:2px solid #d9dde1;
            font-size:12px;
            background-color :#f3f5f7;
            color:rgb(147,153,159)
        .food-item
            display :flex;
            margin:18px;
            padding-bottom:18px;
            border-1px(rgba(7,17,27,0.1));
            &:last-child
                border-none()
                margin-bottom:0;
            .icon
                flex:0 0 57px;
                margin-right :10px;
            .content
                flex:1;
                .name
                    margin:2px 0 8px 0;
                    font-size:14px;
                    height:14px;
                    line-height:14px;
                    color:rgb(7,17,27);
                .desc,.extra
                    line-height:10px;
                    font-size:10px;
                    color:rgb(147,153,159)
                .desc
                    line-height:12px;
                    margin-bottom:8px;
                .extra
                    .count
                        margin-right:12px;
                .price
                    font-weight: 700
                    line-height: 24px
                    .now
                        margin-right: 8px
                        font-size: 14px
                        color: rgb(240, 20, 20)
                    .old
                        text-decoration: line-through
                        font-size: 10px
                        color: rgb(147, 153, 159)    

</style>
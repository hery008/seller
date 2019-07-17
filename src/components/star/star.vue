<template>
    <div class="star" :class="starType">
        <span v-for="(itemClass,index) in itemClasses" :key="index" :class="itemClass" class="star-item"></span>
    </div>
</template>

<script>
    export default {
        props:{
            size:{
                type:Number
            },
            scort:{
                type:Number
            }
        },
        computed:{
            starType(){
                return 'star-' + this.size
            }
        }
    }
</script>

<style lang="stylus" rel="stylesheet/stylus">
.star
    .star-item
        display:inline-block;
        background-repeat:no-repeat;
    &.star-48
    &.star-36
    &.star-24
</style>
<template>
  <div class="header">
    <div class="content-wrapper">
        <div class="avatar">
            <img :src="seller.avatar" width="64" height="64" alt="" />
        </div>
        <div class="content">
            <div class="title">
                <span class="brand"></span>
                <span class="name">{{seller.name}}</span>
            </div>
            <div class="description">
                {{seller.description}}/{{seller.deliveryTime}}分钟送达
            </div>
            <div class="support" v-if="seller.supports">
                <span class="icon" :class="classMap[seller.supports[1].type]"></span>
                <span class="text">{{seller.supports[1].description}}</span>
            </div>
        </div>
        <div class="support-count" v-if="seller.supports" @click="showDetail">
            <span class="count">{{seller.supports.length}}个</span>
            <i class="icon-keyboard_arrow_right"></i>
        </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
        <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
        <span class="icon-keyboard_arrow_right"></span>
    </div>
    <div class="background">
        <img :src="seller.avatar" width="100%" height="100%" alt="" />
    </div>
    <transition name="fade">
        <div class="detail" v-show="detailShow">
            <div class="detail-wrapper clearfix">
                <div class="detail-main">
                    <h1 class="name">{{seller.name}}</h1>
                    <div class="star-wrapper">
                        <star :size="48" :score="seller.score"></star>
                    </div>
                    <div class="title">
                        <div class="line"></div>
                        <div class="text">优惠信息</div>
                        <div class="line"></div>
                    </div>
                    <ul class="supports" v-if="seller.supports">
                        <li class="support-item" v-for="(item,index) in seller.supports">
                            <span class="icon" :class="classMap[item.type]"></span>
                            <span class="text">{{item.description}}</span>
                        </li>
                    </ul>
                    <div class="title">
                        <div class="line"></div>
                        <div class="text">商家公告</div>
                        <div class="line"></div>
                    </div>
                    <div class="bulletin">
                        <p class="content">{{seller.bulletin}}</p>
                    </div>
                </div>
            </div>
            <div class="detail-close" @click="hideDetail">
                <i class="icon-close"></i>
            </div>
        </div>
    </transition>
  </div>
</template>

<script>
  import star from '@/components/star/star'

  export default {
    props:{
        seller:{
            type:Object
        }
    },
    data(){
        return{
            detailShow:false
        }
    },
    methods:{
        showDetail(){
            this.detailShow = true;
        },
        hideDetail(){
            this.detailShow = false;
        }
    },
    created(){
        this.classMap = ['decrease','discount','special','invoice','guarantee'];
    },
    components:{
        star
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import "../../common/stylus/mixins.styl"

.header
    position relative
    color #fff
    background-color rgba(7,17,27,.5)
    overflow hidden
    .content-wrapper
        position relative
        padding 24px 12px 18px 24px
        font-size 0
        .avatar
            display inline-block
            vertical-align top
            img
                border-radius 2px
        .content
            display inline-block
            margin-left 16px
            .title
                margin 2px 0 8px
                .brand
                    display inline-block
                    vertical-align top
                    width 30px
                    height 18px
                    bg-image("brand")
                    background-size 30px 18px
                    background-repeat no-repeat
                .name
                    margin-left 6px
                    font-size 16px
                    line-height 18px
                    font-weight bold
            .description
                margin-bottom 10px
                font-size 12px
            .support
                margin-bottom 2px
                .icon
                    display inline-block
                    vertical-align top
                    width 12px
                    height 12px
                    margin-right 4px
                    background-size 12px 12px
                    background-repeat no-repeat
                    &.decrease
                        bg-image('decrease_1')
                    &.discount
                        bg-image('discount_1')
                    &.guarantee
                        bg-image('guarantee_1')
                    &.invoice
                        bg-image('invoice_1')
                    &.special
                        bg-image('special_1')
                .text
                    vertical-align top
                    font-size 10px
                    line-height 12px
        .support-count
            position absolute
            right 12px
            bottom 14px
            height 24px
            padding 0 8px
            line-height 24px
            border-radius 14px
            background-color rgba(0,0,0,.2)
            text-align center
            .count
                vertical-align top
                font-size 10px
            .icon-keyboard_arrow_right
                margin-left 2px
                line-height 24px
                font-size 10px
    .bulletin-wrapper
        position relative
        height 28px
        line-height 28px
        padding 0 22px 0 12px
        white-space nowrap
        text-overflow ellipsis
        overflow hidden
        background-color rgba(7,17,27,.2)
        .bulletin-title
            display inline-block
            margin-top 8px
            vertical-align top
            width 22px
            height 12px
            bg-image('bulletin')
            background-repeat no-repeat
            background-size 22px 12px
        .bulletin-text
            margin 0 4px
            vertical-align top
            font-size 10px
        .icon-keyboard_arrow_right
            position absolute
            right 12px
            top 9px
            font-size 10px
    .background
        position absolute
        top 0
        left 0
        z-index -1
        width 100%
        height 100%
        filter blur(10px)
    .detail
        position fixed
        top 0
        right 0
        bottom 0
        left 0
        z-index 100
        overflow auto
        background-color rgba(7,17,27,.8)
        backdrop-filter blur(10px)
        &.fade-enter-active,&.fade-leave-active
            transition all .5s
        &.fade-enter,&.fade-leave-active
            opacity 0
        .detail-wrapper
            min-height 100%
            width 100%
            .detail-main
                margin-top 64px
                padding-bottom 64px
                .name
                    line-height 16px
                    font-size 16px
                    font-weight 700
                    text-align center
                .star-wrapper
                    margin-top 18px
                    padding 2px 0
                    text-align center
                .title
                    display flex
                    width 80%
                    margin 28px auto 24px
                    .line
                        flex 1
                        position relative
                        top -6px
                        border-bottom 1px solid rgba(255,255,255,.2)
                    .text
                        padding 0 12px
                        font-size 14px
                        font-weight 700
                .supports
                    width 80%
                    margin 0 auto
                    .support-item
                        padding 0 12px
                        margin-bottom 12px
                        font-size 0
                        &:last-child
                            margin-bottom 0
                        .icon
                            display inline-block
                            width 16px
                            height 16px
                            margin-right 6px
                            vertical-align top
                            background-size 16px 16px
                            background-repeat no-repeat
                            &.decrease
                                bg-image('decrease_2')
                            &.discount
                                bg-image('discount_2')
                            &.guarantee
                                bg-image('guarantee_2')
                            &.invoice
                                bg-image('invoice_2')
                            &.special
                                bg-image('special_2')
                        .text
                            line-height 16px
                            font-size 12px
                .bulletin
                    width 80%
                    margin 0 auto
                    .content
                        padding 0 12px
                        line-height 24px
                        font-size 12px
        .detail-close
            position relative
            width 32px
            height 32px
            margin -64px auto 0
            clear both
            font-size 32px
            

</style>

<template>
  <section class="msite">
    <!--首页头部-->
    <HeaderTop title="昌平区北七家宏福科技园(337省道北)">
      <span class="header_search" slot="left">
        <i class="iconfont icon-sousuo"></i>
      </span>
      <span class="header_login" solt="right">
        <span class="header_login_text">登录|注册</span>
      </span>
    </HeaderTop>
    <!--首页导航-->
    <nav class="msite_nav">
      <div class="swiper-container">
        <div class="swiper-wrapper">
          <div class="swiper-slide">
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/1.jpg">
              </div>
              <span>甜品饮品</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/2.jpg">
              </div>
              <span>商超便利</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/3.jpg">
              </div>
              <span>美食</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/4.jpg">
              </div>
              <span>简餐</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/5.jpg">
              </div>
              <span>新店特惠</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/6.jpg">
              </div>
              <span>准时达</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/7.jpg">
              </div>
              <span>预订早餐</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/8.jpg">
              </div>
              <span>土豪推荐</span>
            </a>
          </div>
          <div class="swiper-slide">
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/9.jpg">
              </div>
              <span>甜品饮品</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/10.jpg">
              </div>
              <span>商超便利</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/11.jpg">
              </div>
              <span>美食</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/12.jpg">
              </div>
              <span>简餐</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/13.jpg">
              </div>
              <span>新店特惠</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/14.jpg">
              </div>
              <span>准时达</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/1.jpg">
              </div>
              <span>预订早餐</span>
            </a>
            <a href="javascript:" class="link_to_food">
              <div class="food_container">
                <img src="./images/nav/2.jpg">
              </div>
              <span>土豪推荐</span>
            </a>
          </div>
        </div>
        <!-- Add Pagination -->
        <div class="swiper-pagination"></div>
      </div>
    </nav>
    <!--首页附近商家-->
    <div class="msite_shop_list">
      <div class="shop_header">
        <i class="iconfont icon-xuanxiang"></i>
        <span class="shop_header_title">附近商家</span>
      </div>
      <ShopList/>
    </div>
</section>
</template>

<script>
import Swiper from 'swiper'
// 同时引入swiper的css文件
import 'swiper/dist/css/swiper.min.css'

import HeaderTop from '../../components/HeaderTop/HeaderTop.vue'
import ShopList from '../../components/ShopList/ShopList.vue'
// 利用mapState语法糖去读取state对象
import {mapState} from 'vuex'
export default {
  data () {
    return {
      baseImageUrl: 'https://fuss10.elemecdn.com'
    }
  },
  components: {
    HeaderTop,
    ShopList
  },
  computed: {
    ...mapState(['address', 'categorys', 'userInfo']),

    /*
    根据categorys一维数组生成一个2维数组
    小数组中的元素个数最大是8
    */
    categorysArr () {
      // 1.先从当前组件中得到所有食品分类的一维数组
      const {categorys} = this
      // 2.准备一个空的二维数组--categorysArr
      const arr = []
      // for (let i = 0, len = categorys.length; i < len; i += 8) {
      //   arr.push(categorys.slice(i, i + 8))
      // }
      // 3.准备一个小数组--pages(最大长度为8)
      let minArr = []
      // 4.遍历categorys得到处理后的二维数组catagorysArr
      categorys.forEach(data => {
        // 如果当前小数组(pages)已经满了, 创建一个新的
        if (minArr.length === 8) {
          minArr = []
        }
        // 如果minArr是空的, 将小数组(pages)保存到大数组(categorysArr)中
        if (minArr.length === 0) {
          arr.push(minArr)
        }
        // 将当前分类信息保存到小数组(pages)中
        minArr.push(data)
      })
      return arr
    }
  },
  // watch: {
  //   categorys (value) { // categorys数组中有数据了 但界面还没有异步更新
  //     // 使用setTimeout可以实现效果, 但是时机不准确
  //     /*
  //     setTimeout(() => {
  //       // 创建一个Swiper实例对象来实现轮播
  //       new Swiper('.swiper-container', {
  //         autoplay: true,
  //         // 如果需要分页器
  //         pagination: {
  //           el: '.swiper-pagination',
  //           clickable: true
  //         }
  //       })
  //     }, 100) */

  //     // 在修改数据之后立即使用它，然后等待 DOM 更新。
  //     this.$nextTick(() => {
  //       // 一旦完成界面更新, 立即执行回调
  //       new Swiper('.swiper-container', {
  //         autoplay: true,
  //         pagination: {
  //           el: '.swiper-pagination',
  //           clickable: true
  //         }
  //       })

  //       // new BScroll('.miste-content-wrapper', {
  //       //   click: true
  //       // })
  //     })
  //   }
  // },
  // 注意要在页面加载完成之后（mounted）再进行swiper的初始化
  mounted () {
    new Swiper('.swiper-container', {
      loop: true, // 可以循环轮播
      // 如果需要分页器
      pagination: {
        el: '.swiper-pagination'
      }
    // 忘记方法名时查看Action.js
    // this.$store.dispatch('getCategorys')
    // this.$store.dispatch('getShops')
    })
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixins.styl"
  .msite  //首页
    width 100%
    .msite_nav
      bottom-border-1px(#e4e4e4)
      margin-top 45px
      height 200px
      background #fff
      .swiper-container
        width 100%
        height 100%
        .swiper-wrapper
          width 100%
          height 100%
          .swiper-slide
            display flex
            justify-content center
            align-items flex-start
            flex-wrap wrap
            .link_to_food
              width 25%
              .food_container
                display block
                width 100%
                text-align center
                padding-bottom 10px
                font-size 0
                img
                  display inline-block
                  width 50px
                  height 50px
              span
                display block
                width 100%
                text-align center
                font-size 13px
                color #666
        .swiper-pagination
          >span.swiper-pagination-bullet-active
            background #02a774
    .msite_shop_list
            top-border-1px(#e4e4e4)
            margin-top 10px
            background #fff
            .shop_header
              padding 10px 10px 0
              .shop_icon
                margin-left 5px
                color #999
              .shop_header_title
                color #999
                font-size 14px
                line-height 20px
</style>

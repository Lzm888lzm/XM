<template>
  <div class="index">
    <div class="container">
      <div class="swiper-box"> 
        <div class="nav-menu">
          <ul class="menu-wrap">
            <li class="menu-item">
              <a href="javascript:;">手机 电话卡</a>
              <div class="childern">
                <ul v-for="(item,index) in menuList" v-bind:key="index">
                  <li v-for="(sub,i) in item" v-bind:key="i">
                  <a v-bind:href="sub?'/#/product/'+sub.id:''">
                  <img :src="sub?sub.img:'/imgs/item-box-2.png'"  alt="">
                  {{sub.img?sub.name:'小米9'}}
                </a>
             </li>
                </ul>
              </div>
            </li>
            <li class="menu-item"> 
              <a href="javascript:;">手机盒子</a>
            </li>
            <li class="menu-item">
              <a href="javascript:;">笔记本 显示器</a>
            </li>
             <li class="menu-item">
              <a href="javascript:;">家电 插线板</a>
            </li>
             <li class="menu-item">
              <a href="javascript:;">出行 穿戴</a>
            </li>
             <li class="menu-item">
              <a href="javascript:;">智能 路由器</a>
            </li>
             <li class="menu-item">
              <a href="javascript:;">电源 配件</a>
            </li>
            <li class="menu-item">
              <a href="javascript:;">耳机 音箱</a>
            </li>
             <li class="menu-item">
              <a href="javascript:;">生活 箱包</a>
            </li>
          </ul>
        </div>
        <swiper v-bind:options="swiperOption">
          <swiper-slide v-for="(item,index) in slideList" v-bind:key="index">
            <a v-bind:href="'/#/product/'+item.id"><img v-bind:src="item.img"></a>
          </swiper-slide>
          <div class="swiper-pagination" slot="pagination"></div>
          <div class="swiper-button-prev" slot="button-prev"></div>
          <div class="swiper-button-next" slot="button-next"></div>
          </swiper>
      </div>
      <div class="ads-box">
          <a :href="'/#/product/'+item.id" v-for="(item,index) in dasList" v-bind:key="index">
            <img v-lazy="item.img" alt="">
          </a>
      </div>
      <div class="banner">
        <a href="/#/product/30">
            <img v-lazy="'/imgs/banner-1.png'" alt="">
          </a>
      </div>
      <div class="product-box">
        <div class="container">
           <h2>手机</h2>
        <div class="weapper">
          <div class="banner-left">
            <a href="/#/product/35"><img v-lazy="'/imgs/mix-alpha.jpg'" alt=""></a>
          </div>
          <div class="list-box">
            <div class="list" v-for="(arr,i) in phoenList" :key="i">
              <div class="item" v-for="(item,j) in arr" :key="j">
                <span v-bind:class="{'new-pro':j%2==0}">新品</span>
                <div class="item-img">
                 <img v-bind:src="item.mainImage" alt="">
                </div>
                <div class="item-info">
                  <h3>{{item.name}}</h3>
                  <p>{{item.subtitle}}</p>
                  <p class="price" @click="addCart(item.id)">{{item.price}}元</p>
                </div>
              </div>
            </div>
          </div>
        </div>
        </div>
      
      </div>
    </div>
    <service-bar></service-bar>
    <modal title="提示"
     suerText="查看购物车"
    btnType="1" 
    modalType="middle" 
    v-bind:showModal="showModal"
    @submit="goToCart"
    @cancel="showModal=false"
    >
    <template v-slot:body>
      商品添加成功
      </template>
      </modal>
  </div>
</template>
<script>

import ServiceBar from '../components/ServiceBar';
import Modal from '../components/Modal';
import { swiper, swiperSlide } from 'vue-awesome-swiper'
import 'swiper/dist/css/swiper.css'
export default {
  naem:"index",
  components:{
    swiper,
    swiperSlide,
    ServiceBar,
    Modal
  },
  data(){
   return{
      swiperOption:{
        autoplay:true,
        loop:true,
          effect : 'cube',
    cubeEffect: {
    slideShadows: true,
    shadow: true,
    shadowOffset: 100,
    shadowScale: 0.6
   },
   pagination: {
    el: '.swiper-pagination',
    clickable:true
   },
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },

      },
      slideList:[
      {
        id:'42',
        img:'/imgs/slider/slide-1.jpg'
      },
       {
        id:'45',
        img:'/imgs/slider/slide-2.jpg'
      },
       {
        id:'46',
        img:'/imgs/slider/slide-3.jpg'
      },
       {
        id:'',
        img:'/imgs/slider/slide-4.jpg'
      },
       {
        id:'',
        img:'/imgs/slider/slide-5.jpg'
      },
      ],
      menuList:[
          [
            {
              id:30,
              img:'/imgs/item-box-1.png',
              name:'小米CC9',
            },{
              id:31,
              img:'/imgs/item-box-2.png',
              name:'小米8青春版',
            },{
              id:32,
              img:'/imgs/item-box-3.jpg',
              name:'Redmi K20 Pro',
            },{
              id:33,
              img:'/imgs/item-box-4.jpg',
              name:'移动4G专区',
            }
          ],
        ],
        dasList:[
          {
            id:33,
            img:"/imgs/ads/ads-1.png"
          },
          {
            id:48,
            img:"/imgs/ads/ads-2.jpg"
          },
          {
            id:45,
            img:"/imgs/ads/ads-3.png"
          },
          {
            id:47,
            img:"/imgs/ads/ads-4.jpg"
          },
        ],
       phoenList:[],
       showModal:false
   }
  },
  //挂载后调用方法
   mounted(){
     this.init()
   },
   //方法
   methods: {
     init(){
       //get 请求       //数据库名称
       this.axios.get('/products',{
         //get获取方法 传参
         params:{
          categoryId:100012, 
          pageSize:14
         }
       }).then((res)=>{
           res.list=res.list.slice(6,14)                    //  切割
          this.phoenList=[res.list.slice(0,4),res.list.slice(4,8),]
       })
     },
     addCart(id){
     
     this.axios.post('/carts',{
         productId:id,
         selected:true
       }).then((res)=>{
           this.showModal=true
           this.$store.dispatch('saveCartCount',res.cartTotalQuantity);
       }).catch(()=>{
        this.showModal=true
       })
     },
     goToCart(){
   this.$router.push('/cart')
     }
   }
}
</script>
<style lang="scss" scoped>
@import './../assets/scss/mixin.scss';
  .index{
    .swiper-box{
      .nav-menu{
        position: absolute;
        width: 264px;
        height:460px;
        z-index: 9;
        padding: 5px 0;
        background: #55585a7a;
        box-sizing: border-box;
        .menu-wrap{
          .menu-item{
           height: 50px;
           line-height: 50px;
           a{
            position: relative;
             display:block;
             font-size: 16px;
             color:#fff ;
            padding-left:30px ;
            &:before{
              position: absolute;
              right: 30px;
              top: 17.5px;
              content: "";
             @include bgImg(10px,15px,'/imgs/icon-arrow.png')
            }
           }
           &:hover{
             background: #ff6600;
               display: block;
              .childern{
                display: block;
              }
           }
           .childern{
             display: none;
             width: 962px;
             height: 451px;
             background: #fff;
             position: absolute;
             padding: 4px 0;
             top: 0;
            left: 264px;
            border: 1px solid #e5e5e5;
            display: none;
            ul{
              display: flex;
              justify-content: space-between;
              height: 75px;
              li{
                height: 75px;
                line-height: 75px;
                flex: 1;  
              }
                 img{
                  width:42px;
                  height:35px;
                  vertical-align:middle;
                  margin-right:15px;
                }
                a{
                  color: #333;
                }
            }
           }
          }
        }
      }
       .swiper-container{
         .swiper-button-prev{
           left: 274px;
         }
         height: 451px
         img{
           width: 100%;
           height: 100%;
        }
       }
    }
    .ads-box{
     @include flex();
      margin-top:14px ;
      margin-bottom: 7px;
     
      a{
        width: 296px;
        height: 167px;
      }
    }
    .banner{
      margin-bottom: 50px;
    }
    .product-box{
      background: #f5f5f5;
      padding: 30px 0px 50px;
      h2{
        color: #333;
        font-size: 22px;
        height: 21px;
        line-height: 21px;
        margin-bottom:20px ;
      }
      .weapper{
        display: flex;
        .banner-left{
          margin-right: 16px;
          img{
            width: 224px;
            height: 619px;
          }
        }
        .list-box{
          .list{
            @include flex();
            width: 986px;
            margin-bottom: 14px;
            &:last-child{
              margin-bottom: 0px;
            }
            .item{
              width: 236px;
              height: 302px;
              background: #fff;
              text-align: center;
              span{
               display: inline-block;
               width: 67px;
               height: 24px;
               font-size: 14px;
               line-height: 24px;
               color: #fff;
               margin-top:5px ;
               &.new-pro{
                background: #7ecf68;
               }
               &.kill-pro{
                 background: #e82626;
               }
              }
              .item-img{
                img{
                  height: 190px;
                  width: 100%;
                }
              }
              .item-info{
                h3{
                font-size: 14px;
                color: #333;
                line-height: 14px;
                font-weight: bold;
                }
              }
              p{
                color: #333;
                line-height: 13px;
                margin: 6px auto 13px;
              }
              .price{
               color:#f20a0a ;
               font-size: 14px;
               font-weight: bold;
               cursor: pointer;
               &:after{
                 @include bgImg(22px,22px,'/imgs/icon-cart-hover.png');
                 content: "";
                 margin-left:5px ;
                 vertical-align: middle;
               }
              }
            }

          }
        }
      }
    }
  }
</style>
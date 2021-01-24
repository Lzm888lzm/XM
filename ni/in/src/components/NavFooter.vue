<template>
  <div class="footer">
   <div class="footer-logo">
     <img src="/imgs/logo-footer.png" alt="">
     <p>小米商城</p>
   </div>
 <div class="footer-link">
   <a href="">河畔一角主页</a><span>|</span>
   <a href="">Vue全栈课程</a><span>|</span>
   <a href="">Reac全家桶课程</a><span>|</span>
   <a href="">河畔一角主页河畔一角主页河畔一角主页河畔一角主页</a>
 </div>
 <div class="copyright">河畔一角主页河畔一角 <span class="domain">主页河畔一角主</span>页河畔一角主页</div>
  </div>
</template>
<script>
export default {
  name:'nav-footer'
}
</script>
<style lang="scss" sceopd>
   .footer{
      height:234px;
      border-top:4px solid #ff6600 ;
      background: #333;
      color: #999;
      font-size: 16px;
      text-align: center;
      .footer-logo{
        margin-top: 46px;
        margin-bottom:31px;
        img{
          width: 53px;
          height: 36px;
          margin-bottom: 13px;
        }
      }
      .footer-link{
        a{
          color: #999;
          display: inline-block;
        }
        span{
          margin: 0 10px;
        }
      margin-bottom: 13px;
      }
      .copyright{
        .domain{
          color: #ff6600;
        } 
       }
   }
</style>
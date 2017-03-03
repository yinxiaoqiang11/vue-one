<template>
  <div class="footer">
    <div class="fooleft">
      <div class="b_cicle">
        <div class="s_cicle">
          <img src="../../../resource/img/555.png" alt="">
        </div>
      </div>
        <strong>￥0</strong>
      <span>另需配送费￥4元</span>
    </div>
    <div class="fooright">
      <h3>￥20起送</h3>
    </div>
  </div>
</template>
<script>

</script>
<style>
  .footer{
    position:absolute;
    bottom:0;
    left:0;
    width:100%;
    height:48px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .footer .fooleft{
    flex-grow:0.72;
    background-color: #141d27;
    height: 48px;
  }

  .footer .fooleft .b_cicle{
    width:54px;
    height:54px;
    /*padding:5px;*/
    border:1px #141d27 solid;
    background-color: #141d27;
    border-radius: 50%;
    position: absolute;
    bottom:5px;
    left:12px;
  }

  .footer .fooleft .s_cicle{
    width:44px;
    height:44px;
    z-index: 10;
    border-radius: 50%;
    border:1px #141d27 solid;
    position: absolute;
    bottom:5px;
    left:5px;
    background-color:#2b343d;
    text-align:center;
    line-height:44px;
  }

  .footer .fooleft img{
    width:22px;
    height:22px;
    margin-top:10px;
  }

  .footer .fooleft strong{
    padding-left: 21.333333vw;
    font-size: 16px;
    color:rgba(255,255,255,0.4);
    font-weight: 1000;
    line-height: 48px;
  }
  .footer .fooleft span{
    padding-left:3.066667vw ;
    font-size: 16px;
    color: rgba(255,255,255,0.4);
    line-height: 48px;
  }

  .footer .fooright{
    flex-grow:0.28;
    background-color: #2b333b;
    height: 48px;
  }
  .footer .fooright h3{
    font-size: 12px;
    color:rgba(255,255,255,0.4);
    font-weight:700;
    line-height: 30px;
    text-align: center;
  }






</style>
﻿<!--<script src="../../assets/js/loginVerify.js"></script>
<script src="../../assets/js/app_product.js"></script>
<script src="../../assets/js/retail_cofirmBuying.js"></script>
<script src="../../assets/js/kandan.js"></script>-->

<script>
	//css引入

  import '../../assets/css/discount.css';

	  export default {
        name: 'kandan',
        data() {
            return {
                msg: 'this is FreeApliy',
                note : {
                  backgroundImage : "url(" + require("../../assets/images/retail-goodsDetails-img004.png") + ")",
                  backgroundRepeat: "no-repeat",
                  backgroundSize: "cover",
                  marginTop: "5px",
                }
            }
        },
      mounted : function () {
        var screenH = window.innerHeight;
        var len = $(".js_banerBigImg img").length;
        for(var j=0;j<len;j++){
          var imgH = $(".js_banerBigImg img").eq(j).height();
          if(imgH>screenH){
            $(".js_banerBigImg img").eq(j).css({width:"auto",height:"100%"})
          }else {
            $(".js_banerBigImg img").eq(j).css({width:"100%",height:"auto"})
          }
        }
        //点击获取验证码判断：手机号码格式是否正确/是否已申请过/是否是合伙人
        $(".get-code-text").click(function(){
          if(!$(this).hasClass("get-code-again")){
            /*显示语言验证码*/
            time(this);
            $('.voice-code-text').show();
            var v = $(".register-phone-number").val();
            if(!isphone3(v)){
              discountSuccess();
              $(".discount-success").text("请输入正确的手机号码");
            }else if(v == "13265565717"){   //已经申请过且申请未被同意
              discountSuccess();
              $(".discount-success").text("你已经申请过了，请等待审核");
            }else if(v == "13265565716"){   //手机号对应的最高身份是推广人或员工
              /*$(".js_com_black").show();
               $(".js_storeP_alert").show();*/
            }else {
              if(v == "13265565715"){    //该用户已经是该店的推广人或者普通用户
                /*$("#js_newUser").hide();*/
                $("#js_newUser").find(".js_input").attr("aria-invalid","false");
              }else if(v == "13265565718"){ //该账户未存在，没有注册过
                /*$("#js_newUser").show();*/
                $("#js_newUser").find(".js_input").attr("aria-invalid","true");
              }
            }
          }
        });
        $(".click-to-get").click(function(){//!reg.test($("#password").val())
          if(!$(this).hasClass("disabled")){
            var reg = /^(?!^(\d+|[a-zA-Z]+)$)(?!.*[~@#]+.*).+$/;
            if($(".register-code").val()!="123456") {  //判断验证码不正确时
              $(".discount-success").text("验证码过期或错误，请重新获取");
              discountSuccess();
            }else if($(".register-phone-number").val()=="15811714179"){      //该用户已经是该店的老板
              /*$(".js_comBlack").show();
               $(".js_storeSelect_alert").show();*/
            }
          }
        });
      }

	  }
</script>


<template>
  <div id="discountMysteryGift">
    <div class="discount-mystery-gift">
      <div class="mystery-gift-nav">
        <img class="mystery-gift-top" src="../../assets/images/mystery_gift_top.png" alt="">
        <img class="mystery-gift-finger" src="../../assets/images/mystery_gift_finger.png" alt="">
        <div class="mystery-friend-send-wrap">
                <span class="discount-top-img discount-top-send" :style="note">
                    <span class="mystery-friend-send">好友赠言</span>
                </span>
          <div class="discount-top-send-right">
            <span class="discount-speak">马格瑞拉：</span>
            <div class="discount-languges">情信送不成，就送这个吧，千言万语在其中。</div>
          </div>
        </div>
        <!--神秘礼物-->
        <div style="display: block">
          <div class="has-discount-left discount-has-time" >
            <div class="not-get">
              <img class="discount-not-get" src="../../assets/images/discount_no_get1.png" alt="">
              <span class="discount-money-wrap">
                            <span class="discount-money">￥</span>
                            <span class="discount-price">900</span>
                        </span>
              <span class="full-money-reduce">满100000可减</span>
            </div>
            <div class="has-discount-right">
              <div class="discount-name"><span class="full-reduce">满减券</span></div>
              <div class="discount-effect">指定商品可用</div>
              <div class="check-discount-wrap discount-time">
                <span>2017.9.30</span><span class="discount-time-min">15:21</span>—
                <span>2017.7.30</span><span class="discount-time-min">17:31</span>
              </div>
              <!--礼物被领取的标识-->
              <img class="already-pass already-pass-robbed already-geted " src="../../assets/images/already_get.png" alt="">
            </div>
          </div>
          <!--在神秘礼物页面被显示-->
          <div style="display: none">
            <div class="discount-warn" >
              注意：接受之后就能看到TA的使用方法了
            </div>
            <div class="mystery-gift-content-wrap">
              <img class="mystery-gift-content" src="../../assets/images/mystery_gift_content.png" alt="">
            </div>
            <div class="accept-him-wrap"><span class="accept-him" onclick="discountSuccess()">接受TA</span></div>
          </div>
        </div>
        <!--神秘礼物end-->
        <!--神秘礼物被抢走-->
        <div style="display: none">
          <div class="has-discount-left discount-has-time" >
            <div class="not-get">
              <img class="discount-not-get" src="../../assets/images/discount_already_pass1.png" alt="">
              <span class="discount-money-wrap">
                            <span class="discount-money">￥</span>
                            <span class="discount-price">900</span>
                        </span>
              <span class="full-money-reduce">满100000可减</span>
            </div>
            <div class="has-discount-right">
              <div class="discount-name"><span class="full-reduce">满减券</span></div>
              <div class="discount-effect">指定商品可用</div>
              <div class="check-discount-wrap discount-time">
                <span>2017.9.30</span><span class="discount-time-min">15:21</span>—
                <span>2017.7.30</span><span class="discount-time-min">17:31</span>
              </div>
              <!--过期的标识别-->
              <img class="already-pass already-pass-robbed" src="../../assets/images/already_pass.jpg" alt="">
            </div>
          </div>
        </div>
        <div class="mystery-gift-content-wrap" style="display: none">
          <img class="mystery-gift-content" src="../../assets/images/lift_robbed.png" alt="">
        </div>
        <!--神秘礼物被抢走字样-->
        <div class="robbe-gift-name" style="display: none">
          TA的礼物被一个叫
          <span class="width-kong"></span>
          李逍遥的人抢走了
          <span class="discount-top-img discount-top-send robbe-gift-header" :style="note"></span>
        </div>
        <!--神秘礼物过期字样-->
        <div class="robbe-gift-name" style="display:none ">
          过期了，都是因为你
        </div>
        <!--神秘礼物已经使用的字样-->
        <div class="robbe-gift-name" style="display:none ">
          你太慢了，TA自己消化了
        </div>
        <!--礼物领取成功-->
        <div style="display: none;">
          <div class="mystery-gift-content-wrap">
            <img class="mystery-gift-content" src="../../assets/images/gift_already_getted.png" alt="">
          </div>
          <!--礼物领取成功字样-->
          <div class="gift-already-getted-wrap" >
            <div class="robbe-gift-name gift-already-getted-text" style="display:block ">
              恭喜，礼物券已领取成功！
            </div>
          </div>
        </div>
        <!--查看更多优惠-->
        <div class="accept-him-wrap" style="display: none"><span class="accept-him">查看更多优惠</span></div>
        <!--立即领取-->
        <div class="accept-him-wrap" style="display: none"><span class="accept-him">立即领取</span></div>
        <!--这是登录页面-->
        <div class="discount-register discount-mystery-gift-register" style="display:block;">
          <div class="discount-rules-wrap">
            优惠细则<span class="assass-right"></span>
          </div>
          <input type="text" class="register-phone-number js_input" aria-invalid="true" onkeyup="phone_verify(this,'get-code-text','get-code-again')" value="13265565715" />
          <div>
            <input type="text" class="register-code js_input" aria-invalid="true" onkeyup="verify_code01(this,'register-code','click-to-get')" placeholder="输入验证码" value="123456">
            <input type="button" class="get-code-text" value="获取验证码" />
            <!--<input class="get-code-text get-code-again" value="重新获取(60s)" />-->
          </div>
          <div class="voice-code-text" style="display:none;">收不到短信？点击获取 <span class="voice-code">语音验证码</span></div>
          <div class="click-to-get">
            <span>点击领取&nbsp;&nbsp;买买买 <img class="right-assass" src="../../assets/images/right_assass.png" alt=""></span>
          </div>
        </div>
      </div>
      <!--神秘礼物被抢走end-->
      <!--点击接受他弹出框-->
      <div class="discount-success" style="display: none">
        成功了
      </div>
    </div>
  </div>

</template>
<style>
  html,body{
    width: 100%;
    height: 100%;
  }
  body{
    background: url('../../assets/images/mystery_gift_bg.png') no-repeat center center/cover;
  }
  /*.discount-mystery-gift{
      background: url('../../assets/images/mystery_gift_bg.png') no-repeat center center/cover;
      height: 100%;
      width: 100%;
  }*/
</style>

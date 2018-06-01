<template>
  <div>
    <!-- <div class="feed_header">
        <img src="../assets/btn_back_icon.png" alt="" @click = "$router.go(-1)">
        <span style="font-size:1.125rem;">意见反馈</span>
        <span class="feed_header_span">充值记录</span>
    </div> -->
    <div class="feed_content">
        <div class="feed_more">
            <span>如果你遇到任何问题或者有更好的建议和意见，您可以通过下面的意见反馈框描述反馈的问题与建议，我们将尽快给你回复</span>
        </div>
        <div class="feed_textarea">
            <textarea name="" id="" rows=1 cols=27 v-model="textVal">

            </textarea>
        </div>
        <div class="feed_contact">
            <span>我们怎么联系你(电话、qq、微信)任意方式</span>
            <input type="text" placeholder="填写时备注是何种方式" v-model="inputVal">
        </div>
        <div class="ios_feed_button">
            <span @click="draw_pay_buttom">立即提交</span>
        </div>
    </div>   
  </div>
</template>

<script>
import Vue from 'vue'
import { Icon } from 'vant';
import { Toast } from 'mint-ui';
import axios from "axios"
import Qs from 'qs'
Vue.use(Icon);
export default {
    data(){
        return {
            textVal:'',
            inputVal:'',
            access_code:'',
            userid:''
        }
    },
    methods: {
        draw_pay_buttom(){
            // window.location.href = 'my://sendMessage_feedback';
            console.log(this.textVal)
            console.log(this.inputVal)
                let data = {
                access_code:this.access_code,
                userid:this.userid,
                advisecontent:this.textVal,
                contactdetail:this.inputVal
            }
            console.log(data)
               axios.get('http://yue.wojianwang.com:8080/api/api-bin/ywms/advice/operation/insertAdvice.action', { params: data }).then(res => {
                console.log(res.data)
                if(res.data.success == 1){
                    Toast({
                    message: '已完成',
                    position: 'bottom',
                    duration: 5000
                });
                window.location.href = 'my://sendMessage_1';
                }else{
                        Toast({
                        message: res.data.errmsg,
                        position: 'bottom',
                        duration: 5000
                    });
                    window.location.href = 'my://sendMessage_0';
                }
            }).catch(error => {
                Toast({
                    message: '请求出错',
                    position: 'bottom',
                    duration: 5000
                })
                window.location.href = 'my://sendMessage_0';
            })
        }
    },
    mounted(){
        console.log(11.30)
        this.access_code = this.$route.query.access_code
        this.userid = this.$route.query.userid
        console.log(this.access_code)
        console.log(this.userid);
        
    }
}
</script>

<style lang="less">
.feed_header {
    height: 44px;
    background: -webkit-linear-gradient(left, #7a55f3, #2ee2df);
    /* Safari 5.1 - 6.0 */
    background: -o-linear-gradient(right, #7a55f3, #2ee2df);
    /* Opera 11.1 - 12.0 */
    background: -moz-linear-gradient(right, #7a55f3, #2ee2df);
    /* Firefox 3.6 - 15 */
    background: linear-gradient(to right, #7a55f3, #2ee2df);
    color: #FFFFFF;
    line-height: 44px;
    text-align: center;
    img {
    width: .625rem;
    height: 18px;
    position: absolute;
    left: .9375rem;
    top: 13px;
    }
}
.feed_content{  
    background-color: #fff;
    .feed_more{
        background: #fffde2;
        box-sizing: border-box;        
        span{
            display: inline-block;
            font-size: 15px;
            padding: 10px;
            color: #4038a5;
        }
    }
    .feed_textarea{
        padding: 15px 15px;
        border-bottom: 5px solid #f5f5f5;
        textarea{
            width: 100%;
            border: 1px dashed #4038a5;
            min-height: 150px;
            font-size: 14px;
            color: #333333;
            box-sizing: border-box;
            resize: none;
            padding: 10px;            
        }
    }
    .feed_contact{
        padding: 10px 15px 15px 15px;
        span{
            color: #4038a5;
            font-size: 14px;
        }
        input{
            margin-top: 10px;
            box-sizing: border-box;            
            padding-left: 15px;
            width: 100%;
            height: 45px;
            font-size: 14px; 
            background: #f1f1f1;
            border-radius: 6px;  
            border: none;     
        }
    }
  
}
    .ios_feed_button {
            margin-top: 30px;
            height: 45px;
            padding: 0 40px;
            line-height: 45px;
            position: absolute;
            display: inline-block;
            bottom: 80px;
            left: 50%;
            -webkit-transform: translateX(-50%);
            transform: translateX(-50%);
            width: 80%;
        button {
            text-align: center;
            border-radius: 40px;
            width: 100%;
            display: inline-block;
            height: 45px;
            background: -webkit-gradient(linear, left top, right top, from(#7a55f3), to(#2ee2df));
            background: linear-gradient(to right, #7a55f3, #2ee2df);
            color: #ffffff;
            border: none;
            display: inline-block;
            /* width: 80%; */
        }
    }
</style>

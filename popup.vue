<template>
  <view class="custom-popup {{idle&&'idle'}} {{popup&&'active'}} {{type}}">
    <view class="custom-popup-mask"  bindtap="hide"></view>
    <view class="custom-popup-content">
      <slot></slot>
    </view>
  </view>
</template>
<config>
    {
        "component": true
    }
</config>
<script>
Component({
    name:'popup',
    properties:{
      popup:{
        type:Boolean,
        default:false,
         observer(newVal, oldVal, changedPath) {
           if(newVal){
             this.setData({
               idle:false
             })
           }else{
             setTimeout(()=>{
                 this.setData({
                    idle:true
                  })
             },300)
           }
        }
      },
      type:{
        type:String,
        default:""
      }
    },
    data:{
      idle:true
    },
    methods:{
      hide(){
        // 无所谓是否由父组件更新再关闭,先关闭再说。
        this.setData({
          popup:false
        })
        this.triggerEvent("change",false);
      },
      show(){
        this.triggerEvent("change",true);
      },
      toggle(){
        let b = !this.data.popup;
        this.triggerEvent("change",b);
      }
    }
  })
</script>
<style lang="scss">
  .custom-popup {
    /*这个方法失效*/
    /*box-shadow: 0 0 1000rpx rgba(0,0,0,0.5);*/

    // 添加这个是为了动画播放完再加上这个类，如果直接加在.custom-popup下会导致刚播放就-11
    &.idle{
      z-index: -11;
      position: relative;
    }
    

    &.right{
      .custom-popup-content{
        right: 0;
        top: 0;
        bottom: 0;
        left: unset;
        transform: translate3d(100%,0,0);
      }
    }

    &.active{
      z-index: 11;
      .custom-popup-content{
        transform: translate3d(0,0,0);
      }

      .custom-popup-mask{
        display: block;
      }
    }

    .custom-popup-mask{
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: 10;
      background: rgba(0, 0, 0, 0.7);
      display: none;
    }

    .custom-popup-content{
      //padding: 0 20rpx;
      background-color: #fff;
      transform: translate3d(0,100%,0);
      transition:transform 0.3s ease;
      position: fixed;
      z-index: 12;
      bottom: 0;
      left: 0;
      right: 0;


    }


  }
</style>

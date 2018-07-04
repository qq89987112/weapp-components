<style lang="scss" scoped>
    .counter-component{
        border: 1rpx solid #bebebe;
        border-radius: 4rpx;
        display: flex;
        align-items: center;
        align-content: center;
        line-height: 30rpx;

        .sub,.add{
           width: 38rpx;
           height: 30rpx;
           text-align: center;
           display: inline-block;
        }
        .value{
            font-size: 20rpx;
            min-width: 43rpx;
            color: #51576F;
            height: 30rpx;
            border: 1rpx solid;
            text-align: center;
            border-color: transparent #bebebe transparent #bebebe;
        }
    }
</style>
<template>
  <view class="counter-component">
      <view class="sub" bindtap="sub">-</view>
      <view class="value">{{value}}</view>
      <view class="add" bindtap="add">+</view>
  </view>
</template>
<config>
{
    "component": true
}
</config>
<script>

    Component({
        properties:{
            min:{
                type:Number,
                value:0
            },
            max:{
                type:Number,
                value:Infinity
            },
            value:{
                type:Number,
                value:0
            }
        },
        methods:{
            add(){  
                let {value,min,max} = this.data;
                max = max||Infinity;
                value = value + 1;
                value = value > max ? max : value;
                this.triggerEvent("add");
                this.triggerEvent("change",value);
            },
            sub(){
                let {value,min,max} = this.data;
                value = value - 1;
                value = value < min ? min : value;
                this.triggerEvent("sub");
                this.triggerEvent("change",value);
            },
            
        }
    })

 
</script>

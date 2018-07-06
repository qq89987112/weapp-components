<style lang="scss" scoped>

    .checkbox-component{
        display: flex;
        align-items: center;
        &.slot{
            image{
                margin-right: 10rpx;
            }
        }

       image{
           width: 36rpx;
           height: 36rpx;
       }
    }


</style>
<template>
  <view bindtap="onCheck" class="checkbox-component {{type}}">
    <!-- <view class="iconfont {{checked ? 'icon-check':'icon-unchecked'}} {{slot&&'slot'}}"></view> -->
    <image src="{{checked ? checkedImage :unCheckedImage}}"></image>
    <slot></slot>
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
            checked:{
                type:Boolean,
                value:false
            },
            type:{
                type:String,
                value:"" //slot
            },
            checkedImage:{
                type:String,
                value:'/assets/image/选中.png'
            },
            unCheckedImage:{
                type:String,
                value:'/assets/image/还未进行订单状态.png'
            },
            disable:{
                type:Boolean,
                value:false
            }
        },
        data:{
            //   slot:!!this.$slots.default
              slot:false
        },
        methods:{
            onCheck(){
                // this.setData({
                //     checked:!this.data.checked
                // })
                this.triggerEvent("change",!this.data.checked);
            }
        }
    })

 
</script>

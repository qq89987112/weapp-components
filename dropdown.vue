<template>
  <view class="cell-toggle-box">
    <view class="cell" bindtap="onCellClick">
      <icon class="iconfont"></icon>
      <text class="text"><slot name="title"></slot></text>
      <icon class="iconfont icon-down {{height&&'active'}}"></icon>
    </view>
    <view class="toggle-content" style="height:{{height}}px">
      <view class="toggle-content-wrapper">
        <slot></slot>
      </view>
    </view>
  </view>
</template>
<config>
  { "component": true }
</config>
<script>

  Component({
    options: {
      multipleSlots: true // 在组件定义时的选项中启用多slot支持
    },
    data: {
      height: 0
    },
    ready() {
      this.activeHeight = 0;
      this.createSelectorQuery().selectAll('.toggle-content-wrapper').boundingClientRect(rect => {
        this.activeHeight = rect.length && rect[0].height || 0;
      }).exec();
    },
    methods: {
      onCellClick() {
        if (this.height) {
          this.height = 0;
        } else {
          this.height = this.activeHeight;
        }
        this.setData({
          height: this.height
        })
      }
    }

  })
</script>
<style lang="scss">
  .cell-toggle-box{
      .cell + .cell{
        border-top: 1rpx solid #efefef;
      }
      .cell{
        display: flex;
        align-items: center;
        align-content: center;
        padding: 0 30rpx;
        line-height: 2.5em;
        background-color: #fff;
        .icon-down{
          margin-right: 20rpx;
          font-size: 0.8em;
          color: #999;
          transition:  0.3s transform cubic-bezier(0.12, 0.4, 0.29, 1.46);

          &.active{
            transform: rotate(180deg);
          }
        }
        .text{
          flex: 1;
        }
        .icon-right{
          font-size: 0.8em;
          color: #999;
        }
      }

      .toggle-content{
        transition: 0.3s height cubic-bezier(0.12, 0.4, 0.29, 1.46);
        overflow:hidden;
      }
    }
</style>
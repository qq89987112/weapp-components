<template>
  <view class="custom-dialog {{visible&&'active'}}" bindtap="onDialogTap">
    <view class="custom-dialog-content" bindtap="onContentTap">
      <slot></slot>
    </view>
  </view>
</template>
<config>
  { "component": true }
</config>
<script>
  Component({
    name: 'dialog',
    properties: {
      visible: {
        type: null,
        default: false
      }
    },
    methods: {
      onDialogTap(e) {
        if (this.stopProp) {
          this.stopProp = false;
        } else {
          this.hide();
        }
      },
      onContentTap(e) {
        this.stopProp = true;
      },
      hide() {
        // 无所谓是否由父组件更新再关闭,先关闭再说。
        this.setData({
          visible: false
        })
        this.triggerEvent("change", false);
      },
      show() {
        this.triggerEvent("change", true);
      },
      toggle() {
        let b = !this.data.popup;
        this.triggerEvent("change", b);
      }
    }
  })
</script>
<style lang="scss">
  .custom-dialog {
    /*这个方法失效*/
    /*box-shadow: 0 0 1000rpx rgba(0,0,0,0.5);*/
    display: flex;
    position: fixed;
    align-items: center;
    align-content: center;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: transparent;

    animation: back .3s forwards;

    @keyframes active {
      100% {
        z-index: 11;
      }
    }
    @keyframes back {
      100% {
        z-index: -1;
      }
    }

    &.active {
      animation: active .3s forwards;
      background: rgba(0, 0, 0, 0.7);

      .custom-dialog-content {
        transform: scale(1);
      }
    }


    .custom-dialog-content {
      width: 100%;
      padding: 30rpx;
      margin: 0 30rpx;
      background-color: #fff;
      transition: transform 0.3s cubic-bezier(0.12, 0.4, 0.29, 1.46);
      align-self: center;
      transform: scale(0);
      z-index: 12;
      border-radius: 10rpx;
    }
  }
</style>
<style lang="scss" scoped>
    @font-face {
        font-family: "iconfont";
        src:url('data:application/x-font-woff;charset=utf-8;base64,d09GRgABAAAAAAWAAAsAAAAACAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAABHU1VCAAABCAAAADMAAABCsP6z7U9TLzIAAAE8AAAARAAAAFZW7k6xY21hcAAAAYAAAABoAAABnNXQft5nbHlmAAAB6AAAAY4AAAG4BaQIrGhlYWQAAAN4AAAALwAAADYQrWALaGhlYQAAA6gAAAAcAAAAJAfeA4VobXR4AAADxAAAABAAAAAQD+kAAGxvY2EAAAPUAAAACgAAAAoBUgC0bWF4cAAAA+AAAAAfAAAAIAETAF1uYW1lAAAEAAAAAUUAAAJtPlT+fXBvc3QAAAVIAAAANgAAAEoHguaeeJxjYGRgYOBikGPQYWB0cfMJYeBgYGGAAJAMY05meiJQDMoDyrGAaQ4gZoOIAgCKIwNPAHicY2Bk/sU4gYGVgYOpk+kMAwNDP4RmfM1gxMjBwMDEwMrMgBUEpLmmMDgwVLw5ytzwv4EhhrmBoQEozAiSAwAzGQ05eJxjYGBgZWBgYAZiHSBmYWBgzGBgZACBJKAoI1icmYELLM7CYAbkcwAhE5CueBb65uj//ygsEGAEq+AAs5hAJjOyMQwYYBw4q1EBD5g0gfJA4V0BxUAnPguFYFC4vjkKwQzMAA8sE/N4nE1PwUobURS95z3fzMQmk2QmmUkmTjKTaJ5iG+iYxoU0ptBNSxeCdOGyCxEExZ2bLmZTcOEiexcpRcgvuBAKXfUbspGSOj/gtrz6FAQv957FuQfOOSSI/v/h17xGLq3Sa3pPO0Qw1tG2WYhY9ntsHdVYVP2KzWVHxman3eNv4beNipcM+l3fMI0ibDSxEScD2WMSb/pDtoXEC4F6I9h1VpYcPsZiTTa/qY/sB6qtzlJx+Ep9eLldSSLXOs07Tt1xzi1DCIuxhaKNI9/LidyioS5FMahet9ZYC/m6DD7tFaKG8+Wsfxyu+DkgTeE2Inu6XQ7Ker8GnuvUzVLBqgWFznIFp39f1Nx82J2THq67pgvEUxJUplD3lKYPyQ0yPfIHtNkl3oMcYrMJ3wamB6Mp9t79nKkbIRDPZoiFUDezqzsh7q4eEY390XekI0QPj2fCf5+fJBq1N9PeF/yW75OlvUkkg1I3Mkqem1CJIn2MJlmmfmXZ5DdCNVcnao5QZBg+svzwicIYOvk9hdhnFQAAeJxjYGRgYADibXK1bPH8Nl8ZuFkYQODacT52BP2/gYWBuQHI5WBgAokCAPOxCHwAeJxjYGRgYG7438AQw8IAAkCSkQEVsAAARwoCbQQAAAAD6QAABAAAAAQAAAAAAAAAAHYAtADcAAB4nGNgZGBgYGEIZGBlAAEmIOYCQgaG/2A+AwAREgFxAHicZY9NTsMwEIVf+gekEqqoYIfkBWIBKP0Rq25YVGr3XXTfpk6bKokjx63UA3AejsAJOALcgDvwSCebNpbH37x5Y08A3OAHHo7fLfeRPVwyO3INF7gXrlN/EG6QX4SbaONVuEX9TdjHM6bCbXRheYPXuGL2hHdhDx18CNdwjU/hOvUv4Qb5W7iJO/wKt9Dx6sI+5l5XuI1HL/bHVi+cXqnlQcWhySKTOb+CmV7vkoWt0uqca1vEJlODoF9JU51pW91T7NdD5yIVWZOqCas6SYzKrdnq0AUb5/JRrxeJHoQm5Vhj/rbGAo5xBYUlDowxQhhkiMro6DtVZvSvsUPCXntWPc3ndFsU1P9zhQEC9M9cU7qy0nk6T4E9XxtSdXQrbsuelDSRXs1JErJCXta2VELqATZlV44RelzRiT8oZ0j/AAlabsgAAAB4nGNgYoAALgbsgIWRiZGZkYWRlYGxgjU5IzU5W6QoMSUzP6m0pCQ/rzQPLJSawsAAALO+CwgAAA==') format('truetype');
    }

    .checkbox-component{

        &.slot{
            .iconfont{
                margin-right: 10rpx;
            }
        }

        .iconfont {
            font-family:"iconfont" !important;
            
            font-style:normal;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            display: inline-block;
        }

        .icon-check:before { content: "\e655"; }

        .icon-unchecked:before { content: "\ecc5"; }
    }


</style>
<template>
  <view bindtap="onCheck" class="checkbox-component {{type}}">
    <view class="iconfont {{checked ? 'icon-check':'icon-unchecked'}} {{slot&&'slot'}}"></view>
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
                default:false
            },
            type:{
                type:String,
                default:""
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

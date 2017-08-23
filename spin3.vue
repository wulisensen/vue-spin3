<template>
  <div :class="{ 'spin-nested-loading': hasContent }">
    <div :class="{ hide: !spinning }">
      <div :class="mainClasses">
        <span :class="dotClasses">
          <i></i>
          <i></i>
          <i></i>
          <i></i>
        </span>
        <div class="spin-text" v-if="tip" v-text="tip"></div>
      </div>
    </div>
    <div :class="contentClasses" v-if="hasContent">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Spin2',
  props: {
    size: {
      type: String,
      default: ''
    },
    tip: {
      type: String
    },
    spinning: {
      type: Boolean,
      default: true
    },
    noDot: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      hasContent: false
    }
  },
  computed: {
    mainClasses() {
      return [
        'spin',
        'spin-spinning', {
          [`spin-${this.size}`]: this.size,
          'spin-show-text': this.tip
        }
      ]
    },
    contentClasses() {
      return [
        'spin-container', {
          'spin-blur': this.spinning
        }
      ]
    },
    dotClasses() {
      return [{
        'spin-dot': !this.noDot,
        'hide': !!this.noDot
      }]
    }
  },
  mounted() {
    this.hasContent = this.$slots.default !== undefined;
  }
}
</script>

<style scoped>
.hide {
  display: none;
}
.spin {
  color: #108ee9;
  vertical-align: middle;
  text-align: center;
  opacity: 0;
  position: absolute;
  -webkit-transition: -webkit-transform .3s cubic-bezier(.78, .14, .15, .86);
  transition: -webkit-transform .3s cubic-bezier(.78, .14, .15, .86);
  transition: transform .3s cubic-bezier(.78, .14, .15, .86);
  transition: transform .3s cubic-bezier(.78, .14, .15, .86), -webkit-transform .3s cubic-bezier(.78, .14, .15, .86);
  font-size: 12px;
  display: none
}
.spin-spinning {
  opacity: 1;
  position: static;
  display: inline-block
}
.spin-nested-loading {
  position: relative
}
.spin-nested-loading>div>.spin {
  position: absolute;
  height: 100%;
  max-height: 320px;
  width: 100%;
  z-index: 4;
}
.spin-nested-loading>div>.spin .spin-dot {
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -10px
}
.spin-nested-loading>div>.spin .spin-text {
  position: absolute;
  top: 50%;
  width: 100%;
  padding-top: 6px
}
.spin-nested-loading>div>.spin.spin-show-text .spin-dot {
  margin-top: -20px
}
.spin-nested-loading>div>.spin-small .spin-dot {
  margin: -7px
}
.spin-nested-loading>div>.spin-small .spin-text {
  padding-top: 3px
}
.spin-nested-loading>div>.spin-small.spin-show-text .spin-dot {
  margin-top: -17px
}
.spin-nested-loading>div>.spin-large .spin-dot {
  margin: -16px
}
.spin-nested-loading>div>.spin-large .spin-text {
  padding-top: 12px
}
.spin-nested-loading>div>.spin-large.spin-show-text .spin-dot {
  margin-top: -26px
}
.spin-container {
  -webkit-transition: all .3s cubic-bezier(.645, .045, .355, 1);
  transition: all .3s cubic-bezier(.645, .045, .355, 1);
  position: relative
}
.spin-blur {
  overflow: hidden;
  opacity: .7;
  -webkit-filter: blur(.5px);
  filter: blur(.5px);
  -webkit-filter: progid\:DXImageTransform\.Microsoft\.Blur(PixelRadius\=1, MakeShadow\=false);
  filter: progid\:DXImageTransform\.Microsoft\.Blur(PixelRadius\=1, MakeShadow\=false);
  -webkit-transform: translateZ(0)
}
.spin-blur:after {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background: #fff;
  opacity: .3;
  -webkit-transition: all .3s;
  transition: all .3s
}
.spin-tip {
  color: rgba(0, 0, 0, .43)
}
.spin-dot {
  position: relative;
  display: inline-block;
  width: 20px;
  height: 20px;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
  -webkit-animation: antRotate 1.2s infinite linear;
  animation: antRotate 1.2s infinite linear
}
.spin-dot i {
  width: 9px;
  height: 9px;
  border-radius: 100%;
  background-color: #108ee9;
  -webkit-transform: scale(.75);
  -ms-transform: scale(.75);
  transform: scale(.75);
  display: block;
  position: absolute;
  opacity: .3;
  -webkit-animation: antSpinMove 1s infinite linear alternate;
  animation: antSpinMove 1s infinite linear alternate;
  -webkit-transform-origin: 50% 50%;
  -ms-transform-origin: 50% 50%;
  transform-origin: 50% 50%
}
.spin-dot i:first-child {
  left: 0;
  top: 0
}
.spin-dot i:nth-child(2) {
  right: 0;
  top: 0;
  -webkit-animation-delay: .4s;
  animation-delay: .4s
}
.spin-dot i:nth-child(3) {
  right: 0;
  bottom: 0;
  -webkit-animation-delay: .8s;
  animation-delay: .8s
}
.spin-dot i:nth-child(4) {
  left: 0;
  bottom: 0;
  -webkit-animation-delay: 1.2s;
  animation-delay: 1.2s
}
.spin-small .spin-dot {
  width: 14px;
  height: 14px
}
.spin-small .spin-dot i {
  width: 6px;
  height: 6px
}
.spin-large .spin-dot {
  width: 32px;
  height: 32px
}
.spin-large .spin-dot i {
  width: 14px;
  height: 14px
}
.spin.spin-show-text .spin-text {
  display: block
}
@media (-ms-high-contrast:active), (-ms-high-contrast:none) {
  .spin-blur {
    background: #fff;
    opacity: .5
  }
}
@-webkit-keyframes antSpinMove {
  to {
    opacity: 1
  }
}
@keyframes antSpinMove {
  to {
    opacity: 1
  }
}
@-webkit-keyframes antRotate {
  to {
    -webkit-transform: rotate(405deg);
    transform: rotate(405deg)
  }
}
@keyframes antRotate {
  to {
    -webkit-transform: rotate(405deg);
    transform: rotate(405deg)
  }
}
</style>
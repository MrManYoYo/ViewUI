<template>
  <div :class="wrapClasses">
    <div :class='ipWrapClasses'>
      <div :class="itemClasses" v-for='item,index in ipModel' :key='index'>
        <InputIp
          v-model="ipModel[index]"
          @dotClick='dotClickHandle(index)'></InputIp>
        <span :class="dotClasses"></span>
      </div>
    </div>
  </div>
</template>

<script>
  import InputIp from '../input-ip'
  const prefixCls = 'ivu-ip';
  const iconPrefixCls = 'ivu-icon';

  export default {
    name: 'Ip',
    components: { InputIp },
    data() {
      return {
        ipModel: [0, 0, 0, 0]
      }
    },
    computed: {
      wrapClasses () {
        return [
          `${prefixCls}`
        ]
      },
      ipWrapClasses () {
        return [
          `${prefixCls}-wrapper`
        ]
      },
      itemClasses () {
        return [
          `${prefixCls}-item`
        ]
      },
      dotClasses () {
        return [
          `${prefixCls}-dot`
        ]
      }
    },
    methods: {
      dotClickHandle (index) {
        if (this.$children.length > 0 && index < 3) {
          this.$children[index + 1].setFocus()
        }
      }
    }
  }
</script>

<style lang="" scoped>
  
</style>
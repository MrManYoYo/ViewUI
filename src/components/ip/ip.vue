<template>
  <div :class="wrapClasses">
    <div :class='ipWrapClasses'>
      <div :class="itemClasses" v-for='item,index in ipModel' :key='index'>
        <InputIp
          v-model="ipModel[index]"
          @on-change='ipItemChangeHandle($event, index)'
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
    props: {
      value: {
        type: String,
      }
    },
    data() {
      return {
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
      },
      ipModel: {
        get () {
          const nums = this.value.split('.')
          nums.forEach((item, index) => {
            if (!item && typeof item !== '0') {
              nums[index] = null
            } else {
              nums[index] = Number(item)
            }
          })
          return nums
        },
        set (val, arg) {
          // console.log(val)
        }
      }
    },
    watch: {
      value (newVal) {
        if (!newVal) {
          return
        } else if (newVal.split('.').length !== 4) {
          return
        } else if (newVal.split('.').length === 4 && newVal.split('.').join('').length > 12) {
          return
        }
        const nums = this.value.split('.')
        nums.forEach((item, index) => {
          if (!item && typeof item !== '0') {
            nums[index] = null
          } else {
            nums[index] = Number(item)
          }
        })
        this.ipModel = nums
      },
    },
    methods: {
      ipItemChangeHandle (value, index) {
        //
        this.$emit('input', this.ipModel.join('.'))
      },
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
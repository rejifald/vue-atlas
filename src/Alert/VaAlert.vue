<template>
  <div :class="[`${classPrefix}-alert`, `${classPrefix}-alert-${type}`]">
    <div :class="`${classPrefix}-alert-${type}-icon`">
      <va-icon :type="iconType" :icon-style="iconStyle"/>
    </div>
    <div>
      <h1 v-if="title">{{title}}</h1>
      <div>
        <slot/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VaAlert',
  props: {
    title: {
      type: String,
      required: false
    },
    type: {
      type: String,
      default: 'warning',
      required: false,
      validator (v) {
        return ['success', 'info', 'warning', 'danger', 'change'].includes(v)
      }
    },
    classPrefix: {
      type: String,
      default: 'va'
    }
  },
  computed: {
    iconType () {
      let { type } = this

      switch (type) {
        case 'success':
          return 'check-circle'
        case 'info':
          return 'info-circle'
        case 'warning':
          return 'exclamation-circle'
        case 'change':
          return 'question-circle'
        case 'danger':
          return 'exclamation-circle'
      }

      return 'info-circle'
    },
    iconStyle () {
      let { type } = this

      switch (type) {
        case 'success':
          return 'solid'
        case 'info':
          return 'solid'
        case 'warning':
          return 'solid'
        case 'change':
          return 'solid'
        case 'danger':
          return 'solid'
      }

      return 'solid'
    }
  }
}
</script>

<style lang="scss">
.#{$class-prefix}-alert {
  display: flex;
  line-height: 20px;
  overflow-wrap: break-word;
  padding: 15px;
  border-radius: 3px;

  /*
  when not using a title, we want to make sure that
  whatever element comes first, is aligned with the icon.
  typically a p
  */
  *:first-child:not(h1) {
    margin: 0;
    padding: 0;
  }

  h1 {
    display: block;
    font-size: 16px;
    font-weight: 600;
    line-height: 20px;
    margin: 0 0 10px 0;
    padding: 0;
    overflow-wrap: break-word;
  }

  &-warning-icon,
  &-success-icon,
  &-info-icon,
  &-danger-icon,
  &-change-icon {
    display: block;
    flex-basis: auto;
    flex-grow: 0;
    flex-shrink: 0;
    line-height: 20px;
    margin: 0;
    padding: 0;
    overflow-wrap: break-word;
    width: 34px;
    font-size: 18px;
  }

  &-warning {
    background: $Y50;
    &-icon {
      color: $Y500;
    }
  }
  &-success {
    background: $G50;
    &-icon {
      color: $G500;
    }
  }
  &-info {
    background: $B50;
    &-icon {
      color: $B500;
    }
  }
  &-danger {
    background: $R50;
    &-icon {
      color: $R500;
    }
  }
  &-change {
    background: $P50;
    &-icon {
      color: $P500;
    }
  }
}
</style>

<template>
    <div class="zan-cell zan-field"
         :class="{ 'zan-field--error': error , 'zan-field--wrapped': mode === 'wrapped' }">
      <div
        v-if="title"
        :class="{'align-right': rightTitle}"
        class="zan-cell__hd zan-field__title">{{ title }}</div>
      <textarea
        v-if="type === 'textarea'"
        auto-height
        :name="name || componentId || ''"
        :value="value"
        :focus="focus"
        :maxlength="maxLength"
        :key="'textarea-'+componentId"
        :placeholder="placeholder"
        class="zan-field__input zan-cell__bd"
        :class="{ 'zan-field__input--right' : right }"
        placeholder-class="zan-field__placeholder"
        @change="_handleZanFieldChange"
        @focus="_handleZanFieldFocus"
        @blur="_handleZanFieldBlur"
        :data-component-id="componentId || ''"></textarea>
      <input
        v-else
        :type="inputType || 'text'"
        :name="name || componentId || ''"
        :value="value"
        :focus="focus"
        :maxlength="maxLength"
        :key="'input-'+componentId"
        :placeholder="placeholder"
        class="zan-field__input zan-cell__bd"
        :class="{ 'zan-field__input--right' : right }"
        placeholder-class="zan-field__placeholder"
        @change="_handleZanFieldChange"
        @focus="_handleZanFieldFocus"
        @blur="_handleZanFieldBlur"
        :data-component-id="componentId || ''"/>
    </div>
</template>

<script>
  /**
   * 不能用input事件，会导致页面频闪
   * 新增title靠右对齐
   * 新增最大长度
   */
  import {extractComponentId} from '../../utils/helper'
  export default {
    props: {
      error: Boolean,
      mode: String,
      title: String,
      type: String,
      focus: Boolean,
      name: String,
      componentId: String,
      value: String,
      inputType: String,
      rightTitle: Boolean,
      right: Boolean,
      placeholder: String,
      maxLength: Number,
      handleZanFieldChange: Function,
      handleZanFieldFocus: Function,
      handleZanFieldBlur: Function
    },
    methods: {
      _handleZanFieldChange (event) {
        const componentId = extractComponentId(event)
        event.componentId = componentId

        // console.info('[zan:field:change]', event)

        if (this.handleZanFieldChange) {
          return this.handleZanFieldChange(event)
        }

        console.warn('页面缺少 handleZanFieldChange 回调函数')
      },

      _handleZanFieldFocus (event) {
        const componentId = extractComponentId(event)
        event.componentId = componentId

        console.info('[zan:field:focus]', event)

        if (this.handleZanFieldFocus) {
          return this.handleZanFieldFocus(event)
        }

        console.warn('页面缺少 handleZanFieldFocus 回调函数')
      },

      _handleZanFieldBlur (event) {
        const componentId = extractComponentId(event)
        event.componentId = componentId

        // console.info('[zan:field:blur]', event)

        if (this.handleZanFieldBlur) {
          return this.handleZanFieldBlur(event)
        }

        console.warn('页面缺少 handleZanFieldBlur 回调函数')
      }
    }
  }
</script>

<style scoped>

</style>

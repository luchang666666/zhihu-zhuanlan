<template>
    <form class="validate-form-container">
      <slot name="default"></slot>
      <div class="submit-area" @click.prevent="submitForm">
        <slot name="submit">
          <button type="submit" class="btn btn-primary">提交</button>
        </slot>
      </div>
    </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
type ValidateFunc = () => boolean
export default defineComponent({
  name: 'ValidateForm',
  emits: ['form-submit'],
  setup (props, context) {
    const funcArr: ValidateFunc[] = []
    const submitForm = () => {
      const result = funcArr.map(func => func()).every(result => result)
      context.emit('form-submit', true)
    }
    return {
      submitForm
    }
  }
})
</script>

<style scoped>

</style>

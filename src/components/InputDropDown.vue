<template>
  <div class="comp-root">
    <input
      class="focus:outline-none border-b-3 focus:border-green-300 w-full h-full"
      type="text"
      :value="modelValue"
      @input="updateInput($event)"
    />
  </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, toRefs } from 'vue'

let props = defineProps({
  modelValue: String
})

const { modelValue } = toRefs(props)

let emit = defineEmits(['update:modelValue'])

const updateInput = (event: any) => {
  emit('update:modelValue', event.target.value)
}
</script>

<style lang="postcss" scoped>
.comp-root {
}
</style>
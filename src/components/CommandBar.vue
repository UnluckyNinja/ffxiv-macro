<template>
  <div class="comp-root w-full h-10 grid grid-cols-12 gap-2 text-xl border-2 relative">
    <slot></slot>
    <div class="col-span-1">/</div>
    <InputDropDown
      class="col-span-2"
      type="text"
      name="command"
      :modelValue="command"
      @update:modelValue="emitInput('update:command', $event)"
    />
    <InputDropDown
      class="col-span-7"
      type="text"
      name="arguments"
      :modelValue="argumentText"
      @update:modelValue="emitInput('update:argumentText', $event)"
    />
    <button class="col-span-1" @click="emit('moveUp')">▲</button>
    <button class="col-span-1" @click="emit('moveDown')">▼</button>
    <button class="absolute left-full ml-1 w-8 h-8 text-red-400" @click="$emit('delete')">✖</button>
  </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, toRefs } from "vue"
import InputDropDown from './InputDropDown.vue'

const props = defineProps({
  command: String,
  argumentText: String,
})
const emit = defineEmits(['update:command', 'update:argumentText', 'delete', 'moveUp','moveDown'])

const { command, argumentText } = toRefs(props)

const emitInput = (name: Parameters<typeof emit>[0], event: any) => {
  emit(name, event)
}
</script>

<style lang="postcss" scoped>
.comp-root {
  @apply py-px;
}
</style>
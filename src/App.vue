<template>
  <div class="relative h-screen w-screen pt-20 flex">
    <nav class="absolute top-0 left-0 right-0 pt-4 h-20 flex justify-center">
      <h1 class="text-4xl text-center">FFXIV Macro Generator</h1>
    </nav>
    <main class="p-8 h-full w-full overflow-auto flex flex-1">
      <div class="mr-10 grid grid-cols-1 gap-1 flex-1 place-content-start">
        <CommandBar
          class="col-span-1"
          v-for="m, i in macro"
          :key="i"
          v-model:command="m.command"
          v-model:argumentText="m.argumentText"
          @delete="macro.splice(i, 1)"
          @move-up="moveCommandUp(i)"
          @move-down="moveCommandDown(i)"
        >
          <div class="absolute -left-8 w-6 flex items-center justify-end top-0 bottom-0 my-auto text-right select-none"><span>
            {{ i + 1 }}
          </span></div>
        </CommandBar>
        <div
          v-if="macro.length < 15"
          class="w-full h-10 cursor-pointer border-4 border-dashed"
          @click="macro.push({})"
        >
          <div class="h-full flex justify-center text-gray-400 text-2xl">+</div>
        </div>
      </div>
      <!-- output -->
      <div class="flex-1">
        <div class="inline-block pl-8 border text-left">
          <div
            class="bg-gray-100 w-80 h-6 leading-6 border-0 relative cursor-text hover:bg-gray-200"
            v-for="line, i in macroLines"
            :key="i"
          >
            <div class="absolute -left-8 w-8 text-right px-2 select-none">{{ i + 1 }}</div>
            <code class="pl-2 w-full h-full">
              <span class>{{ line }}</span>
            </code>
          </div>
        </div>
        <div>
          <button
            class="m-8 border rounded px-4 py-2 shadow text-3xl bg-green-300"
            @click="copyMacro"
          >复制</button>
        </div>
      </div>
    </main>
    <aside class="flex-none">
      <ActionPanel class="w-60 h-full overflow-hidden"></ActionPanel>
    </aside>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import ActionPanel from '@/components/ActionPanel.vue'
import CommandBar from '@/components/CommandBar.vue'

let macro = ref([{}] as any[])

let macroLines = computed(() => {
  let text = macro.value.map(it => {
    let command = it.command ?? 'echo'
    console.log(`${command}: ${it.command}`)
    return ['/' + command, it.argumentText].join(' ')
  })
  if (macro.value.length < 15) {
    return [...text, ...Array.from(Array(15 - macro.value.length), () => '')]
  }
  return [...text]
})

const copyMacro = () => {
  if (!navigator.clipboard) return
  let text = macro.value.map(it => {
    let command = it.command ?? 'echo'
    console.log(`${command}: ${it.command}`)
    return ['/' + command, it.argumentText].join(' ')
  })

  navigator.clipboard.writeText(text.join('\n'))
}

const moveCommandUp = (index: number) => {
  if (index === 0) return
  let temp = macro.value.splice(index, 1)[0]
  macro.value.splice(index - 1, 0, temp)
}
const moveCommandDown = (index: number) => {
  if (index === macro.value.length - 1) return
  let temp = macro.value.splice(index, 1)[0]
  macro.value.splice(index + 1, 0, temp)
}
</script>

<style lang="postcss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  @apply overflow-hidden;
}
</style>

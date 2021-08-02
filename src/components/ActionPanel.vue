<template>
  <div class="comp-root">
    <div class="general-category">
      <button class="button" @click="category_1 = 'battle'">
        <img src="src/assets/icons/community/activity/Battle.png" />
      </button>
      <button class="button" @click="category_1 = 'crafting'">
        <img src="src/assets/icons/community/activity/Crafting.png" />
      </button>
      <button class="button" @click="category_1 = 'gathering'">
        <img src="src/assets/icons/community/activity/Gathering.png" />
      </button>
      <button class="button" @click="category_1 = 'chatting'">
        <img src="src/assets/icons/community/activity/Chatting.png" />
      </button>
    </div>
    <div class="sub-category">
      <div class="container" v-if="category_1 === 'battle'">
        <button
          class="button w-12 h-12"
          v-for="c, i in battleClasses"
          :key="i"
          @click="category_2 = c.name"
        >
          <div
            class="w-full h-full bg-contain bg-center bg-no-repeat"
            :style="{ 'backgroundImage': 'url(' + c.icon + ')' }"
          ></div>
        </button>
      </div>
      <div class="container" v-else-if="category_1 === 'crafting'">
        <button
          class="button w-12 h-12"
          v-for="c, i in craftClasses"
          :key="i"
          @click="category_2 = c.name"
        >
          <div
            class="w-full h-full bg-contain bg-center bg-no-repeat"
            :style="{ 'backgroundImage': 'url(' + c.icon + ')' }"
          ></div>
        </button>
      </div>
      <div class="container" v-else-if="category_1 === 'gathering'">
        <button
          class="button w-12 h-12"
          v-for="c, i in gatherClasses"
          :key="i"
          @click="category_2 = c.name"
        >
          <div
            class="w-full h-full bg-contain bg-center bg-no-repeat"
            :style="{ 'backgroundImage': 'url(' + c.icon + ')' }"
          ></div>
        </button></div>
      <div class="container" v-else-if="category_1 === 'chatting'"></div>
      <div class="container" v-else>select one</div>
    </div>
    <div class="actions"></div>
  </div>
</template>

<script lang="ts" setup>
// import { useToggle } from '@vueuse/core'

import { ref } from 'vue';

import battleClasses from '@/data/battle'
import craftClasses from '@/data/craft'
import gatherClasses from '@/data/gather'

// const [value, toggle] = useToggle()

let category_1 = ref('battle')
let category_2 = ref('')
</script>

<style lang="postcss" scoped>
.comp-root {
  @apply border-2 divide-y-2 space-y-2;
}

.general-category {
  @apply flex w-full;
  .button {
    @apply flex-1;
    img {
      @apply w-full;
    }
  }
}
.sub-category .container {
  @apply grid grid-cols-4 max-h-60 overflow-auto justify-evenly place-content-start;
}

.btn {
  @apply m-4 p-2 border rounded shadow;
}
</style>
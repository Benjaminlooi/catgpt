<template>
  <div class="w-full border-b border-black/10 dark:border-gray-900/50 text-gray-800 dark:text-gray-100 group  "
    :class="{ 'bg-gray-50 dark:bg-[#444654]': responseType === 'RESPONSE', 'dark:bg-gray-800': responseType === 'INPUT' }">
    <!-- dark:bg-gray-800 -->
    <div class="text-base gap-4 md:gap-6 m-auto md:max-w-2xl lg:max-w-2xl xl:max-w-3xl p-4 md:py-6 flex lg:px-0">
      <div class="w-[30px] flex flex-col relative items-end">
        <div v-if="responseType === 'RESPONSE'"
          class="relative h-[30px] w-[30px] p-1 rounded-sm text-white flex items-center justify-center"
          style="background-color: rgb(16, 163, 127);">
          <CatGptIcon />
        </div>

        <div v-if="responseType === 'INPUT'"
          class="relative h-[30px] w-[30px] p-1 rounded-sm text-gray-600 flex items-center justify-center bg-white">
          <p class="font-bold">B</p>
        </div>
      </div>
      <div class="relative flex w-[calc(100%-50px)] flex-col gap-1 md:gap-3 lg:w-[calc(100%-115px)]">
        <div class="flex flex-grow flex-col gap-3">
          <div class="min-h-[20px] flex flex-col items-start gap-4 whitespace-pre-wrap">
            <div class="markdown prose w-full break-words dark:prose-invert light">
              <p :class="{ 'generating-response': generatingWord }">{{ word }}</p>
            </div>
          </div>
        </div>
        <FeedbackButtons v-if="responseType === 'RESPONSE'" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Message } from '~~/types';

const props = defineProps<{
  message: Message
}>()

const responseType = computed(() => props.message.type)

// split words from message.text and display a new word every 1-2 seconds
const words = props.message.text.split(' ')
const word = ref('')
const wordIndex = ref(0)
const generatingWord = ref(false)

onMounted(() => {
  if (responseType.value === 'RESPONSE') {
    loop()
  } else if (responseType.value === 'INPUT') {
    word.value = props.message.text
  }
})

function loop() {
  generatingWord.value = true

  const timeout = setTimeout(() => {
    word.value += words[wordIndex.value] + ' '
    wordIndex.value++
    if (wordIndex.value === words.length) {
      generatingWord.value = false
      clearTimeout(timeout)
    } else {
      loop()
    }
  }, Math.floor(Math.random() * 600) + 10)
}



</script>

<style scoped lang="scss">
.generating-response::after {
  animation: blink 1s steps(5, start) infinite;
  content: "▋";
  margin-left: 0.25rem rem;
  vertical-align: baseline;
}

// blingking animation
@keyframes blink {

  0%,
  80% {
    opacity: 1;
  }

  100% {
    opacity: 0;
  }
}
</style>
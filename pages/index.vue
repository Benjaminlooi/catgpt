<template>
  <div class="overflow-hidden w-full h-screen relative">
    <div class="flex flex-1 flex-col h-full md:pl-[260px]">
      <main class="relative h-screen w-full transition-width flex flex-col overflow-hidden items-stretch flex-1">
        <div class="flex-1 overflow-hidden">
          <div class="react-scroll-to-bottom--css-mebvg-79elbk h-full dark:bg-gray-800">
            <div class="react-scroll-to-bottom--css-mebvg-1n7m0yu">
              <div class="flex flex-col items-center text-sm dark:bg-gray-800">
                <WelcomeMessage v-if="messages.length === 0" />
                <ResponseMessage v-for="message of messages" :message="message" />
                <div class="w-full h-32 md:h-48 flex-shrink-0"></div>
              </div>
            </div>
          </div>
        </div>
        <div
          class="absolute bottom-0 left-0 w-full border-t md:border-t-0 dark:border-white/20 md:border-transparent md:dark:border-transparent md:bg-vert-light-gradient bg-white dark:bg-gray-800 md:!bg-transparent dark:md:bg-vert-dark-gradient">
          <form class="stretch mx-2 flex flex-row gap-3 pt-2 last:mb-2 md:last:mb-6 lg:mx-auto lg:max-w-3xl lg:pt-6">
            <div class="relative flex h-full flex-1 md:flex-col">
              <!-- Regenerate Response Button -->
              <!-- <div class="flex ml-1 mt-1.5 md:w-full md:m-auto md:mb-2 gap-0 md:gap-2 justify-center"><button
              class="btn flex justify-center gap-2 btn-neutral border-0 md:border"><svg stroke="currentColor" fill="none"
                stroke-width="1.5" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-3 w-3"
                height="1em" width="1em" xmlns="http://www.w3.org/2000/svg">
                <polyline points="1 4 1 10 7 10"></polyline>
                <polyline points="23 20 23 14 17 14"></polyline>
                <path d="M20.49 9A9 9 0 0 0 5.64 5.64L1 10m22 4l-4.64 4.36A9 9 0 0 1 3.51 15"></path>
              </svg>
              Regenerate response
            </button>
          </div> -->
              <div
                class="flex flex-col w-full py-2 flex-grow md:py-3 md:pl-4 relative border border-black/10 bg-white dark:border-gray-900/50 dark:text-white dark:bg-gray-700 rounded-md shadow-[0_0_10px_rgba(0,0,0,0.10)] dark:shadow-[0_0_15px_rgba(0,0,0,0.10)]">
                <textarea @keydown.enter="submitInput" v-model="input" tabindex="0"
                  style="max-height: 200px; height: 24px; overflow-y: hidden;" rows="1"
                  class="m-0 w-full resize-none border-0 bg-transparent p-0 pl-2 pr-7 focus:outline-0 focus:ring-0 focus-visible:ring-0 dark:bg-transparent md:pl-0"></textarea>
                <button
                  class="absolute p-1 rounded-md text-gray-500 bottom-1.5 right-1 md:bottom-2.5 md:right-2 hover:bg-gray-100 dark:hover:text-gray-400 dark:hover:bg-gray-900 disabled:hover:bg-transparent dark:disabled:hover:bg-transparent">
                  <svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round"
                    stroke-linejoin="round" class="h-4 w-4 mr-1" height="1em" width="1em"
                    xmlns="http://www.w3.org/2000/svg">
                    <line x1="22" y1="2" x2="11" y2="13"></line>
                    <polygon points="22 2 15 22 11 13 2 9 22 2"></polygon>
                  </svg>
                </button>
              </div>
            </div>
          </form>
          <div class="px-3 pt-2 pb-3 text-center text-xs text-black/50 dark:text-white/50 md:px-4 md:pt-3 md:pb-6"><a
              href="" target="_blank" rel="noreferrer" class="underline">CatGPT Feb 21 Version</a>. Free Research Preview.
            Our goal is
            to make AI systems more natural
            and safe to interact with. Your feedback will help us Meow.</div>
        </div>
      </main>
    </div>
    <TheSidebar />
  </div>
</template>

<script setup lang="ts">
import { Message } from '~~/types';

const responseMessageOne: Ref<Message> = ref({
  id: 0,
  text: `test`,
  type: 'INPUT',
})

const responseMessageTwo: Ref<Message> = ref({
  id: 0,
  text: `Hello! Is there anything you'd like me to help you with?`,
  type: 'RESPONSE',
})

const messages: Ref<Message[]> = ref([]);

const input = ref('');

function submitInput() {
  if (input.value === '') return;

  const newText = input.value.replace(/(\r\n|\n|\r)/gm, "");
  const newMessage: Message = {
    id: messages.value.length,
    text: newText,
    type: 'INPUT',
  };
  messages.value.push(newMessage);
  input.value = '';

  generateResponse()
}

function generateResponse() {
  const response = 'Meow '.repeat(Math.floor(Math.random() * 10) + 2);
  
  const newMessage: Message = {
    id: messages.value.length,
    text: response,
    type: 'RESPONSE',
  };
  messages.value.push(newMessage);
}

</script>

<style lang="scss" scoped></style>
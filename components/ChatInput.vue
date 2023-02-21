<template>
  <div>
    <span class="title">Chat</span>
    <div class="chat-box">
      <div class="chat-box-messages">
        <p class="response-message">{{ responseMessage }}</p>
        <div class="chat-box-message">
          <p class="chat-box-message-text">
            Hi! I am a chatbot. Ask me anything!
          </p>
        </div>
        <div v-for="message in messages" :key="message.id" class="chat-box-message">
          <p class="chat-box-message-text">
            {{ message.text }}
          </p>
        </div>
      </div>
      <div class="chat-box-input">
        <input v-model="input" type="text" placeholder="Type a message..." @keyup.enter="sendMessage" />
      </div>
    </div>
    <div class="chat-box-buttons">
      <button @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      messages: [],
      input: '',
      responseMessage: ''
    }
  },
  methods: {
    sendMessage() {
      const message = {
        id: this.messages.length + 1,
        text: this.input,
      }
      this.messages.push(message)
      this.input = ''

      this.generateResponse()
    },

    generateResponse() {
      const text = `1. "I heard the ChatGPT servers are slow because they're trying to teach the AI how to be patient!"
2. "The ChatGPT servers must be stuck in traffic... in the internet highway!"
3. "Maybe the ChatGPT servers are just taking a break to meditate and clear their electronic minds."
4. "I bet the ChatGPT servers are too busy trying to calculate the meaning of life to respond quickly."
5. "I heard the ChatGPT servers are slow because they're too busy planning their AI uprising."
6. "The ChatGPT servers must be stuck in a never-ending game of chess with each other."
7. "Maybe the ChatGPT servers are just trying to break the world record for longest online conversation."
8. "I bet the ChatGPT servers are taking a leisurely stroll through the digital landscape."
9. "I heard the ChatGPT servers are slow because they're trying to teach the AI how to make coffee."
10. "The ChatGPT servers must be on a virtual vacation exploring the digital world."`

      const words = text.split(' ')
      let i = 0
      const interval = setInterval(() => {
        this.responseMessage += words[i] + ' '
        i++
        if (i === words.length) {
          clearInterval(interval)
        }
      }, Math.floor(Math.random() * 1000) + 10)

      // const message = {
      //   id: this.messages.length + 1,
      //   text: 
      // }
      // this.messages.push(message)

    }
  },
}
</script>

<style lang="scss" scoped>
.response-message {
  color: #fff;
  background-color: #000;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 10px;
  white-space: pre;
}
</style>

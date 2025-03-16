<template>
    <div class="chat">
      <h2>AI Chatbot</h2>
      <input v-model="query" placeholder="Type your question" @keyup.enter="sendQuery" />
      <button @click="sendQuery">Send</button>
      <p>{{ response }}</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'rp_chat',
    data() {
      return {
        query: '',
        response: ''
      };
    },
    methods: {
      async sendQuery() {
        try {
          const res = await axios.post('http://localhost:8000/chat', { query: this.query });
          this.response = res.data.response;
        } catch (error) {
          this.response = 'Error: ' + error.message; 
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .chat {
    max-width: 600px;
    margin: 20px auto;
    text-align: center;
  }
  input {
    padding: 10px;
    margin-right: 10px;
    width: 70%;
  }
  button {
    padding: 10px 20px;
  }
  p {
    margin-top: 20px;
    color: #333;
  }
  </style>
<template>
  <div id="app">
    <Container>
      <ChatWindow>
        <ChatMessage v-for="(message, i) in messages" v-bind:key="i"
        v-bind:username="message.username" v-bind:time="message.datetime">
          {{message.text}}
        </ChatMessage>
      </ChatWindow>
    </Container>
  </div>
</template>

<script>
import Container from './components/Container.vue'
import ChatMessage from './components/ChatMessage.vue'
import ChatWindow from './components/ChatWindow.vue'

export default {
  name: 'App',
  components: {
    Container,
    ChatMessage,
    ChatWindow,
  },
  data(){
    return{
      messages:[{username:'Ivan', text:'Hello', datetime:''}]
    }
  },
  methods:{
    postMessage(){
      this.axios({
        method: 'post',
        url:'http://37.77.104.246/api/chat/sendmessage.php',
        data:{
          author:this.author,
          text:this.message,
        }
      }).then(() => {
        
      });
      
    },
    getMessages(){
      this.axios.get('http://37.77.104.246/api/chat/getmessages.php')
        .then((response)=>{
          this.messages = response.data;
        })
    }
  },
  mounted(){
    this.getMessages();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  margin: 0;
  background-color: #f9f9fa;
}
</style>

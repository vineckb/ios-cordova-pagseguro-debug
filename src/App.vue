<template>
  <div id="app">
    <p>Session ID: {{ session }}</p>
    <p>Sender Hash: {{ senderHash }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      session: '',
      senderHash: ''
    }
  },

  mounted() {
    axios.get('https://simba.mufasa.com.br/api.11lub.com.br/public/api/pagseguro').then(response => {
      const javascript = document.createElement("script");
      javascript.setAttribute("src", response.data.javascript);
      document.head.appendChild(javascript);

      javascript.onload = () => {
        this.session = response.data.session_id;
        window.PagSeguroDirectPayment.setSessionId(response.data.session_id);

        window.PagSeguroDirectPayment.onSenderHashReady(response => {
          if (!response || response.status === 'error') {
            alert('Erro ao instanciar integração com pagseguro, reinicie o app para prosseguir com o pagamento');
            return false;
          }
          this.senderHash = response.senderHash;
        });
      };
    });
  },
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
</style>

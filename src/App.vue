<template>
  <div id="app">
    <label for="houser">Houser</label>
    <input type="text" id="houser" v-model="houser" />
    <input type="text" v-model="message" />
    <button @click="send">Send</button>
    <p>
      {{ api }}
    </p>
    <p>
      {{ message }}
    </p>
    <p>
      {{ response }}
    </p>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    houser: 1,
    message: "",
    response: [],
  }),
  computed: {
    api() {
      return "wss://35.224.222.17:8000/ws/v1/orders/houser/" + this.houser;
    },
  },
  created: function () {
    console.log("Starting connection to WebSocket Server");
    this.connection = new WebSocket(this.api);

    this.connection.onmessage = function (event) {
      console.log(event);
    };

    this.connection.onopen = function (event) {
      console.log(event);
      console.log("Successfully connected to the echo websocket server...");
    };
  },
  methods: {
    send() {},
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

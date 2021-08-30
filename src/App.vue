<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { PushNotifications } from "@capacitor/push-notifications";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  async created() {
    PushNotifications.createChannel({
      id: "start",
      description: "hihi world",
      sound: "a",
      importance: 4,
    });

    PushNotifications.requestPermissions().then(function (re) {

      if (re.receive === "granted") {
        PushNotifications.register();
      }
    });

    PushNotifications.addListener("registration", async function (token) {

      console.log(token["value"]);

      
    });

    
    PushNotifications.addListener("pushNotificationReceived", (notice) => {

      console.log(JSON.stringify(notice));

    });
  },
};
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

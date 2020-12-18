<template>
  <div>
    <form @submit.prevent="connect">
      <label
        >AppID:
        <input type="text" v-model="appId" />
      </label>
      <br />
      <label
        >Endpoint:
        <input type="text" v-model="endpoint" />
      </label>
      <br />
      <button>Connect</button>
    </form>
    <form @submit.prevent="login">
      <label
        >Email:
        <input type="email" v-model="email" />
      </label>
      <br />
      <label
        >Password:
        <input type="password" v-model="password" />
      </label>
      <br />
      <button>Login</button>
    </form>
  </div>
</template>
<script>
import * as Appwrite from "appwrite";

export default {
  name: "Login",
  data() {
    return {
      appId: "",
      endpoint: "",
      email: "",
      password: ""
    };
  },
  methods: {
    connect() {
      const appwrite = new Appwrite()
        .setEndpoint(this.endpoint)
        .setProject(this.appId);
      console.log({ appwrite });
      Object.assign(this, { appwrite });
    },
    login() {
      this.appwrite.account
        .createSession(this.email, this.password)
        .then(res => console.log(res))
        .catch(err => console.log(err));
    }
  }
};
</script>

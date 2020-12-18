<template>
  <form @submit.prevent="connect">
    <div class="field">
      <label class="label">AppID</label>
      <div class="control">
        <input
          v-model="appId"
          class="input"
          type="text"
          placeholder="5fdcff85ebb12"
        />
      </div>
    </div>

    <div class="field">
      <label class="label">Endpoint</label>
      <div class="control">
        <input
          v-model="endpoint"
          class="input"
          type="email"
          placeholder="http://localhost/v1"
        />
      </div>
    </div>

    <div class="field">
      <label class="label">Email</label>
      <div class="control">
        <input
          v-model="email"
          class="input"
          type="text"
          placeholder="example@email.addr"
        />
      </div>
    </div>

    <div class="field">
      <label class="label">Password</label>
      <div class="control">
        <input
          v-model="password"
          class="input"
          type="email"
          placeholder="a_$ecUre*pAssw0r6"
        />
      </div>
    </div>
  </form>
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
        .then(res => {
          console.log(res);
          this.$router.push("/dash");
        })
        .catch(err => console.log(err));
    }
  }
};
</script>

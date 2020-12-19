<template>
  <div class="login is-flex is-justify-content-center">
    <form @submit.prevent="login">
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
            type="text"
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
            type="email"
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
            type="password"
            placeholder="a_$ecUre*pAssw0r6"
          />
        </div>
      </div>
      <button class="button is-primary">Login</button>
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
    login() {
      const appwrite = new Appwrite()
        .setEndpoint(this.endpoint)
        .setProject(this.appId);
      Object.assign(this, { appwrite });

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

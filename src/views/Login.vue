<template>
  <form>
    <label
      >AppID:
      <input name="app" />
    </label>
    <button>Save</button>
  </form>
</template>
<script>
export default {
  name: "Login",
  data() {
    return {
      appId: ""
    };
  }
};
</script>

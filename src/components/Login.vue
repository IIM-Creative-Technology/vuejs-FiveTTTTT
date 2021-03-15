<template>
  <div id="login">
    <form action="">
      <p>Nom</p>
      <input type="text" />
      <br />

      <p>Email</p>
      <input type="email" name="" id="" />
      <br />

      <p>mot de passe</p>
      <input type="password" name="" id="" />
      <br />

      <p>vérification du mot de passe</p>
      <input type="password" name="" id="" />
      <br />

      <input type="button" value="Se connecter" v-on:click="connection(true)" />
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    connection(index) {
      this.$emit("connection", { isConnected: index });
    },
  },
};
</script>

<style>
#login form {
  display: flex;
  flex-direction: column;
  width: 50%;
  margin: auto;
  margin-top: 20vh;
  border-radius: 10px;
  padding: 20px;
  background-color: rgb(114, 114, 114);
}
#login form input {
  width: 60%;
  margin: auto;
  border-radius: 5px;
}
#login {
  position: absolute;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.6);
}
</style>
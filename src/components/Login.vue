<template>
  <div id="login">
    <form action="">
      <p>Nom</p>
      <input type="text" id="theName" required/>
      <br />

      <p>Email</p>
      <input type="email" name="" id="theEmail" required />
      <br />

      <p>mot de passe</p>
      <input type="password" name="" id="thePass" required />
      <br />

      <p>vérification du mot de passe</p>
      <input type="password" name="" id="passVerif" required />
      <p id="wrongPass" style="display: none; color: red">
        Ce n'est pas le même mot de passe
      </p>
      <br />

      <input
        type="submit"
        value="Se connecter"
        v-on:click="verification(true)"
        required
      />
    </form>
    <button v-if="isConnected" v-on:click="deconection">Se deconnecter</button>
  </div>
</template>

<script>
export default {
  props: ["isConnected"],
  methods: {
    deconection() {
      // this.$emit("connection", { isConnected: index });
    },
    verification(index) {
      let name = document.getElementById("theName").value;
      let email = document.getElementById("theEmail").value;
      let password = document.getElementById("thePass").value;
      let passVerif = document.getElementById("passVerif").value;

      // console.log("aya " + passVerif);
      // console.log("name: " + name);
      // console.log("email: " + email);
      // console.log("password: " + password);

      if (password != passVerif && password != "" && passVerif != "") {
        document.getElementById("wrongPass").style.display = "block";
      } else {
        this.connection(index);
        this.sendNewUser(name, email, password);
      }
    },
    connection(index) {
      this.$emit("connection", { isConnected: index });

      // if (
      //   document.getElementById("pass") == document.getElementById("passVerif")
      // ) {
      //   this.$emit("connection", { isConnected: index });
      // } else {
      //   document.getElementById("wrongPass").style.display = "block";
      // }
    },
    sendNewUser(name, email, password) {
      // console.log("name: " + name);
      // console.log("email: " + email);
      // console.log("password: " + password);
      this.$emit("sendNewUser", {
        name: name,
        email: email,
        password: password,
      });
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
  /* margin-top: 20vh; */
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
  /* background-color: rgba(0, 0, 0, 0.6); */
}
</style>
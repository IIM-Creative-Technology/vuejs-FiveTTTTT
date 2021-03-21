<template>
  <div id="login" v-if="theUser.name == ''">
    <form action="">
      <p>Nom</p>
      {{ theUser.name }}
      <input type="text" id="theName" required />
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
  </div>
  <div id="logout" v-else>
    <h2>Vous êtes connecté</h2>
    <br /><br />
    <button v-on:click="deconection">Se deconnecter</button>
  </div>
</template>

<script>
export default {
  props: ["theUser"],
  methods: {
    deconection() {
      this.$emit("deconnection", { name: "" });
    },
    verification() {
      let name = document.getElementById("theName").value;
      let email = document.getElementById("theEmail").value;
      let password = document.getElementById("thePass").value;
      let passVerif = document.getElementById("passVerif").value;

      if (password != passVerif || password == "" || passVerif == "") {
        if (password != passVerif) {
          document.getElementById("wrongPass").style.display = "block";
        }
      } else {
        this.sendNewUser(name, email, password);
      }
    },
    sendNewUser(name, email, password) {
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
#login form,
#logout {
  display: flex;
  flex-direction: column;
  width: 50%;
  margin: auto;
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
}

#logout button {
  width: 50%;
  margin: auto;
}
</style>
<template>
  <header>
    <div id="nav">
      <router-link to="/Admin" v-if="theUser.name != ''"
        >Gérer le blog<span> | </span>
      </router-link>
      <router-link to="/Blog">Blog</router-link> |
      <router-link to="/login">Connexion</router-link>
    </div>
    <!-- seulement si on est connecte, on va etre salué -->
    <div v-if="theUser.name != ''">Bonjour, {{ theUser.name }}</div>
  </header>

  <!-- on va echanger (recevoir(v-on) et envoyer(v-bind)) des actions ou des variables avec les composants en utilisant router-view -->
  <router-view
    @editBlog="changeArticle"
    @createArticle="addArticle"
    @deconnection="deconnection"
    @sendNewUser="changeUser"
    v-bind:blogs="blogs"
    v-bind:theUser="theUser"
  />
</template>


<script lang="ts">
export default {
  name: "App",
  data() {
    return {
      theUser: {
        name: "a",
        email: "",
        password: "",
      },

      // comme je n'arrivai pas à ajouter un element à une liste vide j'ai du creer un de base
      blogs: [
        {
          content: "Cet article a été créer pour que vous le modifiez",
          title: "mon blog test",
          metaTitle: "mon_premier_blog",
          metaDescription: "ouais",
          date: "17/03/2021",
          user: "test",
        },
        {
          content: "Cet article a été créer pour que vous le modifiez",
          title: "z",
          metaTitle: "mon_premier_blog",
          metaDescription: "ouais",
          date: "17/03/2021",
          user: "test",
        },
        {
          content: "Cet article a été créer pour que vous le modifiez",
          title: "a",
          metaTitle: "mon_premier_blog",
          metaDescription: "ouais",
          date: "17/03/2021",
          user: "test",
        },
      ],
    };
  },
  methods: {
    deconnection(payload) {
      this.name = payload.name;
      this.theUser.name = this.name;
    },

    changeUser(payload) {
      this.name = payload.name;
      this.email = payload.email;
      this.password = payload.password;

      let newName = this.name;
      let newEmail = this.email;
      let newPass = this.password;

      this.theUser.name = newName;
      this.theUser.email = newEmail;
      this.theUser.password = newPass;
    },

    addArticle(payload) {
      let theBlog = this.blogs;
      theBlog.push(payload.article);
    },

    changeArticle(payload) {
      this.thecontent = payload.content;
      this.theMetaTitle = payload.metaTitle;
      this.theMetaDescription = payload.metaDescription;
      this.user = payload.user;

      this.blogs[payload.article].metaTitle = this.theMetaTitle;
      this.blogs[payload.article].metaDescription = this.theMetaDescription;
      this.blogs[payload.article].content = this.thecontent;
      this.blogs[payload.article].user = this.user;
    },
  },
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
}
body {
  background-color: rgb(48, 48, 48);
  position: relative;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #d3d3d3;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a span {
  text-decoration: none;
  color: white;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.nouvBlog h3 {
  overflow: hidden;
  text-decoration: underline;
  height: 4vh;
  width: 50%;
}

header {
  display: flex;
  justify-content: space-between;
}
header div {
  padding: 30px;
}
</style>

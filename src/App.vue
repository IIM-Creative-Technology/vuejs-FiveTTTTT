<template>
  <header>
    <div id="nav">
      <router-link to="/Admin" v-if="theUser.name != ''"
        >Gérer le blog<span> | </span>
      </router-link>
      <router-link to="/">Blog</router-link> |
      <router-link to="/login">Connexion</router-link>
      <!-- <router-link to="/login">Login</router-link> -->
    </div>
    <div v-if="theUser.name != ''">Bonjour, {{ theUser.name }}</div>
  </header>
  <router-view
    @editBlog="changeArticle"
    @createArticle="addArticle"
    @deconnection="deconnection"
    @sendNewUser="changeUser"
    v-bind:blogs="blogs"
    v-bind:isConnected="isConnected"
    v-bind:theUser="theUser"
  />
</template>


<script lang="ts">
// import Admin from "./components/Admin.vue";
// import Login from "./components/Login.vue";

export default {
  name: "App",
  data() {
    return {
      isConnected: false,
      theUser: {
        name: "",
        email: "admin@admin.fr",
        password: "1234",
      },

      blogs: [
        {
          theImages: 1,
          content: "Cet article a été créer pour que vous le modifiez",
          title: "mon blog test",
          metaTitle: "mon_premier_blog",
          metaDescription: "ouais",
          date: "17/03/2021",
          user: "moi",
        },
        // {
        //   theImages: 2,
        //   content: "ipsum",
        //   title: "mon deuxieme blog",
        //   metaTitle: "mon_deuxieme_blog",
        //   metaDescription: "ouais",
        //   date: 17032021,
        //   user: "moi",
        // },
        // {
        //   theImages: 3,
        //   content: "sincuae",
        //   title: "mon troisieme blog",
        //   metaTitle: "mon_troisieme_blog",
        //   metaDescription: "ouais",
        //   date: 17032021,
        //   user: "moi",
        // },
        // {
        //   theImages: 4,
        //   content: "premium",
        //   title: "mon quatrieme blog",
        //   metaTitle: "mon_quatrieme_blog",
        //   metaDescription: "ouais",
        //   date: 17032021,
        //   user: "moi",
        // },
      ],
    };
  },
  components: {
    // Admin,
    // Login,
  },
  methods: {
    // connection(payload) {
    //   this.isConnected = payload.name;
    //   // console.log("co");
    //   // console.log("co " + payload.name);
    // },
    deconnection(payload) {
      this.name = payload.name;
      // this.isConnected = payload.name;
      this.theUser.name = this.name;
      // console.log("co");
      // console.log("co " + payload.name);
    },
    changeUser(payload) {
      // console.log("cos");

      this.name = payload.name;
      this.email = payload.email;
      this.password = payload.password;
      let newName = this.name;
      let newEmail = this.email;
      let newPass = this.password;
      // console.log("nameNew : " + newName);
      // console.log("emailNew : " + newEmail);
      // console.log("passwordNew : " + newPass);

      this.theUser.name = newName;

      this.theUser.email = newEmail;

      this.theUser.password = newPass;
    },
    addArticle(payload) {
      let theBlog = this.blogs;
      theBlog.push(payload.article);
      // console.log("wsh ca marche");
      // let newLi = document.getElementById("");
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
    // removeBlog(payload) {
    //   this.removerId = payload.removerId;
    //   let idCheck = this.removerId;
    //   let removeThisBlog = this.blogs;
    //   removeThisBlog.splice(idCheck, 1);
    // },
    connecting(payload) {
      this.isConnected = payload.isConnected;
      let popUpCo = document.getElementById("login");
      popUpCo.style.display = "none";
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

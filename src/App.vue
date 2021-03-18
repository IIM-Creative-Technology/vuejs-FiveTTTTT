<template>
  <Login @connection="connecting" v-if="!isConnected" />
  <div id="nav">
    <router-link to="/Admin">Gérer le blog</router-link> |
    <router-link to="/blog">Blog</router-link>
    <!-- <router-link to="/login">Login</router-link> -->
  </div>
  <router-view @editBlog="changeArticle" v-bind:blogs="blogs" />
  <!-- <Admin @remover="removeBlog" v-bind:blogs="blogs" /> -->
</template>


<script lang="ts">
// import Admin from "./components/Admin.vue";
import Login from "./components/Login.vue";

export default {
  name: "App",
  data() {
    return {
      isConnected: true,
      blogs: [
        {
          theImages: 1,
          content: "lorem",
          title: "mon premier blog",
          metaTitle: "mon_premier_blog",
          metaDescription: "ouais",
          date: 17032021,
          user: "moi",

        },
        {
          theImages: 2,
          content: "ipsum",
          title: "mon deuxieme blog",
          metaTitle: "mon_deuxieme_blog",
          metaDescription: "ouais",
          date: 17032021,
          user: "moi",
        },
        {
          theImages: 3,
          content: "sincuae",
          title: "mon troisieme blog",
          metaTitle: "mon_troisieme_blog",
          metaDescription: "ouais",
          date: 17032021,
          user: "moi",
        },
        {
          theImages: 4,
          content: "premium",
          title: "mon quatrieme blog",
          metaTitle: "mon_quatrieme_blog",
          metaDescription: "ouais",
          date: 17032021,
          user: "moi",
        },
      ],
    };
  },
  components: {
    // Admin,
    Login,
  },
  methods: {
    changeArticle(payload) {
      this.thecontent = payload.content;
      this.theMetaTitle = payload.metaTitle;
      this.theMetaDescription = payload.metaDescription;
      this.blogs[payload.article].metaTitle = this.theMetaTitle;
      this.blogs[payload.article].metaDescription = this.theMetaDescription;
      this.blogs[payload.article].content = this.thecontent;
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

#nav a.router-link-exact-active {
  color: #42b983;
}

.nouvBlog h3 {
    overflow: hidden;
    text-decoration: underline;
    height: 4vh;
    width: 50%;
}
</style>

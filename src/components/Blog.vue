<template>
  <div id="blog">
    <ul id="myBlogs">
      <li v-for="(blog, index) in blogs" :key="(blog, index)">
        <div v-bind:id="'nouvBlog' + index" class="nouvBlog">
          <img
            src="./../assets/logo.png"
            alt=""
            style="width: 20px; height: 20px"
          />
          <!-- <router-link to="'/blog:'.index"></router-link> -->
          <div v-on:click="showArticle(index)">
            <!-- <div> -->
            <h3>{{ blog.title }}</h3>
            <p>{{ blog.metaDescription }}</p>
          </div>
          <!-- <div class="blogsActions">
            <button v-on:click="openEdit(index)">Editer</button>
            <img
              src="./../assets/trash.png"
              alt=""
              style="width: 20px; height: 20px"
              v-on:click="removeBlog(index)"
            />
          </div> -->
        </div>
      </li>
    </ul>
    <div id="theArticle" style="display: none">
      <img
        src="./../assets/logo.png"
        alt=""
        style="width: 200px; height: 200px"
      />
      <h2 id="theArticleTitle"></h2>
      <p id="theArticleContent"></p>
      <div id="extraInfos">
        <p id="theArticleDate"></p>
        <div id="signature">
          <img
            src="./../assets/logo.png"
            alt=""
            style="width: 30px; height: 30px"
          />
          <p id="theArticleUser"></p>
        </div>
      </div>
    </div>
    <br />

    <!-- <Login /> -->
  </div>
</template>

<script>
// import { defineComponent } from '@vue/composition-api'
// import Login from "../components/Login";

export default {
  name: "Blog",
  props: ["blogs"],
  components: {
    // Login,
  },
  methods: {
    showArticle(index) {
      let menu = document.getElementById("myBlogs");
      let article = document.getElementById("theArticle");

      let title = document.getElementById("theArticleTitle");
      let content = document.getElementById("theArticleContent");
      let date = document.getElementById("theArticleDate");
      let user = document.getElementById("theArticleUser");

      title.innerHTML = this.blogs[index].title;
      content.innerHTML = this.blogs[index].content;
      date.innerHTML = "Dernieres modifications : "+this.blogs[index].date;
      user.innerHTML = this.blogs[index].user;

      menu.style.display = "none";
      article.style.display = "block";
    },
  },
};
</script>

<style>
#extraInfos {
  display: flex;
  justify-content: space-between;
  padding: 60px;
}
#signature {
  display: flex;
  /* justify-content: right;
  align-content: flex-end; */
}
#blog #myBlogs .nouvBlog {
  height: 10vh;
  margin-bottom: 15px;
}
#blog #myBlogs .nouvBlog div {
  width: 65%;
}
</style>

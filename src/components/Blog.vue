<template>
  <div id="blog">
    <h1>Tous vos posts</h1>
    <ul id="myBlogs">
      <li v-for="(blog, index) in blogs" :key="(blog, index)">
        <router-link
          v-bind:to="'/Blog/' + blog.title"
          v-on:click="goToPost(index)"
        >
          <div v-bind:id="'nouvBlog' + index" class="nouvBlog">
            <img
              src="./../assets/logo.png"
              alt=""
              style="width: 20px; height: 20px"
            />
            <div v-on:click="showArticle(index)">
              <h3>{{ blog.title }}</h3>
              <p>{{ blog.metaDescription }}</p>
            </div>
          </div>
        </router-link>
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
    <router-view />
  </div>

  <!-- </router-view> -->
</template>

<script>
export default {
  name: "Blog",
  props: ["blogs"],
  methods: {
    goToPost(index) {
      console.log("index " + index);

      this.$emit("goToPost", {
        index: index,
      });
    },
    showArticle(index) {
      let menu = document.getElementById("myBlogs");
      let article = document.getElementById("theArticle");

      let title = document.getElementById("theArticleTitle");
      let content = document.getElementById("theArticleContent");
      let date = document.getElementById("theArticleDate");
      let user = document.getElementById("theArticleUser");

      title.innerHTML = this.blogs[index].title;
      content.innerHTML = this.blogs[index].content;
      date.innerHTML = "Dernieres modifications : " + this.blogs[index].date;
      user.innerHTML = this.blogs[index].user;

      menu.style.display = "none";
      article.style.display = "block";
    },
  },
};
// this.showArticle(1)
</script>

<style>
#extraInfos {
  display: flex;
  justify-content: space-between;
  padding: 60px;
}
#signature {
  display: flex;
}
#blog #myBlogs .nouvBlog {
  height: 10vh;
  margin-bottom: 15px;
}
#blog #myBlogs .nouvBlog div {
  width: 65%;
}
#myBlogs a{
  text-decoration: none;
  color: white;
}
#theArticleContent {
  width: 80%;
  margin: auto;
}
</style>

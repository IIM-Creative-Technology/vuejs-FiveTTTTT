<template>
  <div id="blog">
    <h1>Tous vos posts</h1>
    <ul id="myBlogs">
      <!-- on affiche chaque article de blogs -->
      <li v-for="(blog, index) in blogs" :key="(blog, index)">
        <router-link v-bind:to="'/Blog/' + blog.title">
          <div v-bind:id="'nouvBlog' + index" class="nouvBlog">
            <img
              src="./../assets/logo.png"
              alt=""
              style="width: 20px; height: 20px"
            />
            <div>
              <h3>{{ blog.title }}</h3>
              <p>{{ blog.metaDescription }}</p>
            </div>
          </div>
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Blog",
  props: ["blogs"],
};
</script>

<style>
h1 {
  margin: 10px;
}
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
#myBlogs a {
  text-decoration: none;
  color: white;
}
#theArticleContent {
  width: 80%;
  margin: auto;
}
</style>

<template>
  <div id="post">
    <img
      src="./../assets/logo.png"
      alt=""
      style="width: 200px; height: 200px"
    />
    <h2 id="theArticleTitle">{{ $route.params.titreDuPost }}</h2>
    <!-- on lance une boucle for pour trouver quel index correspond au nom de l'article -->
    <div v-for="(blog, index) in blogs" :key="(blog, index)">
      <div v-if="blog.title == $route.params.titreDuPost">
        <p id="theArticleContent">{{ blog.content }}</p>
        <div id="extraInfos">
          <p id="theArticleDate">{{ blog.date }}</p>
          <div id="signature">
            <img
              src="./../assets/logo.png"
              alt=""
              style="width: 30px; height: 30px"
            />
            <p id="theArticleUser">{{ blog.user }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["blogs"],
};
</script>

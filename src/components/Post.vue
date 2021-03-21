<template>
  <div id="post">
    <img
      src="./../assets/logo.png"
      alt=""
      style="width: 200px; height: 200px"
    />
    <h2 id="theArticleTitle">{{ $route.params.titreDuPost }}</h2>
    <div v-for="(blog, index) in blogs" :key="(blog, index)">
      <div v-if="blog.title==$route.params.titreDuPost">
        <p id="theArticleContent">{{blog.content}}</p>
        <div id="extraInfos">
          <p id="theArticleDate">{{blog.date}}</p>
          <div id="signature">
            <img
              src="./../assets/logo.png"
              alt=""
              style="width: 30px; height: 30px"
            />
            <p id="theArticleUser">{{blog.user}}</p>
          </div>
        </div>
      </div>
    </div>
    <router-view @goToPost="showInfos" />
  </div>
</template>

<script>
// import { defineComponent } from '@vue/composition-api'
// this.showInfos("content");
export default {
  props: ["blogs"],
  
};
</script>

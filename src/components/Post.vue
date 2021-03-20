<template>
    <div id="post">
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
</template>

<script>
// import { defineComponent } from '@vue/composition-api'

export default {
    props: ["blogs"],

}
</script>

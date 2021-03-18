<template>
  <div id="myAdmin">
    <ul id="myBlogs">
      <li v-for="(blog, index) in blogs" :key="(blog, index)">
        <div v-bind:id="'nouvBlog' + index" class="nouvBlog">
          <img
            src="./../assets/logo.png"
            alt=""
            style="width: 20px; height: 20px"
          />
          <p>{{ blog.title }}</p>
          <div class="blogsActions">
            <button v-on:click="openEdit(index)">Editer</button>
            <img
              src="./../assets/trash.png"
              alt=""
              style="width: 20px; height: 20px"
              v-on:click="removeBlog(index)"
            />
          </div>
        </div>
        <br />
      </li>
    </ul>
    <EditBlog @sendEdit="editBlog" v-bind:index="selectedBlog" />
    <!-- <EditBlog @sendEdit="editBlog" /> -->
  </div>
</template>

<script>
import EditBlog from "./EditBlog.vue";
export default {
  components: {
    EditBlog,
  },
  props: ["blogs"],
  name: "Admin",
  data() {
    return {
      selectedBlog: 0,
    };
  },
  computed: {},
  methods: {
    editBlog(payload) {
      this.thecontent = payload.content;
      let theContent = this.thecontent;
      //   this.thetitle = payload.title;
      this.theMetaTitle = payload.metaTitle;
      let theMetaTitle = payload.metaTitle;
      this.theMetaDescription = payload.metaDescription;
      let theMetaDescription = payload.metaDescription;
      this.$emit("editBlog", {
        article: this.selectedBlog,
        content: theContent,
        metaTitle: theMetaTitle,
        metaDescription: theMetaDescription,
      });
      //   this.blogs[this.selectedBlog].title = this.thetitle;
      // this.blogs[this.selectedBlog].metaTitle=this.theMetaTitle;
      //   this.blogs[this.selectedBlog].metaTitle = this.theMetaTitle;
      //   this.blogs[this.selectedBlog].metaDescription = this.theMetaDescription;
      //   this.blogs[this.selectedBlog].content = this.thecontent;
      //   console.log("wsh");
    },
    removeBlog(index) {
      let editBlog = document.getElementById("editBlog");
      let removeThisBlog = this.blogs;
      let myBlogs = document.getElementById("myBlogs");

      if (this.selectedBlog == index) {
        myBlogs.style.width = "100%";

        let unselectBlog = document.getElementById("nouvBlog" + index);
        unselectBlog.style.backgroundColor = " rgb(75, 75, 75)";
        editBlog.style.display = "none";
      }
      removeThisBlog.splice(index, 1);
    },
    unselect(index) {
      for (let i = 0; i < this.blogs.length; i++) {
        if (i != index) {
          let unselectBlog = document.getElementById("nouvBlog" + i);
          unselectBlog.style.backgroundColor = " rgb(75, 75, 75)";
        }
      }
    },
    openEdit(index) {
      this.selectedBlog = index;
      let nouvBlog = document.getElementById("nouvBlog" + index);
      let myAdmin = document.getElementById("myAdmin");
      let myBlogs = document.getElementById("myBlogs");
      let editBlog = document.getElementById("editBlog");
      let blogContent = document.getElementById("blogContent");
      let blogTitle = document.getElementById("blogTitle");
      let blogMTitle = document.getElementById("blogMTitle");
      let blogMDescription = document.getElementById("blogMDescription");

      nouvBlog.style.backgroundColor = " rgb(121, 121, 121)";

      myBlogs.style.width = "40%";
      myAdmin.style.display = "flex";
      myAdmin.style.justifyContent = "space-around";
      editBlog.style.display = "block";
      editBlog.style.width = "55%";
      blogTitle.innerHTML = this.blogs[index].title;
      blogMTitle.value = this.blogs[index].metaTitle;
      blogMDescription.value = this.blogs[index].metaDescription;
      blogContent.value = this.blogs[index].content;

      this.unselect(index);

      return index;
    },
  },
};
</script>

<style>
#myAdmin {
}
ul {
  list-style: none;
}
.nouvBlog {
  padding: 10px;
  border-radius: 10px;
  width: 80%;
  height: 5vh;
  background-color: rgb(75, 75, 75);
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nouvBlog .blogsActions {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.nouvBlog p {
  overflow: hidden;
  height: 4vh;
  width: 50%;
}
</style>
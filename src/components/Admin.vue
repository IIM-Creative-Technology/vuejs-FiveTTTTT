<template>
  <div v-if="theUser.name == ''">
    <h3>
      Vous n'avez pas accès à cette page. Veuillez allez vous connecter :
      <router-link to="/login" style="color: #42b983">Connexion</router-link>
    </h3>
  </div>
  <div id="Admin" v-else>
    <button v-on:click="openCreate" id="createButton">Créer un article</button>
    <div id="myAdmin">
      <ul id="myBlogs">
        <li v-for="(blog, index) in blogs" :key="(blog, index)">
          <div v-bind:id="'nouvBlog' + index" class="nouvBlog">
            <img
              src="./../assets/logo.png"
              alt=""
              style="width: 20px; height: 20px"
            />
            <h3>{{ blog.title }}</h3>
            <div class="blogsActions">
              <button v-on:click="openEdit(index)" id="editButton">Editer</button>
              <img
                src="./../assets/trash.png"
                alt=""
                style="width: 25px; height: 25px"
                v-on:click="removeBlog(index)"
              />
            </div>
          </div>
          <br />
        </li>
      </ul>
      <EditBlog
        @sendEdit="editBlog"
        @sendCreation="createArticle"
        v-bind:index="selectedBlog"
        v-bind:create="create"
        v-bind:blogs="blogs"
        v-bind:theUser="theUser"
      />
    </div>
  </div>
</template>

<script>
import EditBlog from "./EditBlog.vue";

export default {
  components: {
    EditBlog,
  },
  props: ["blogs", "theUser"],
  name: "Admin",
  data() {
    return {
      selectedBlog: 0,
      create: true,
    };
  },
  computed: {},
  methods: {
    isConnected() {
      if (this.theUser.name == "") {
        alert(
          "Vous ne pouvez pas effectuer cette action car vous n'êtes pas connecté. Veuillez  vous connecter pour continuer."
        );
        return false;
      } else {
        return true;
      }
    },
    createArticle(payload) {
      this.thecontent = payload.content;
      let theContent = this.thecontent;

      this.theTitle = payload.title;
      let theTitle = this.theTitle;

      this.theDate = payload.date;
      let theDate = this.theDate;

      this.theMetaTitle = payload.metaTitle;
      let theMetaTitle = payload.metaTitle;

      this.theMetaDescription = payload.metaDescription;
      let theMetaDescription = payload.metaDescription;

      let newArticle = {
        content: theContent,
        title: theTitle,
        metaTitle: theMetaTitle,
        metaDescription: theMetaDescription,
        date: theDate,
        user: this.theUser.name,
      };

      this.$emit("createArticle", {
        article: newArticle,
      });
    },
    editBlog(payload) {
      this.thecontent = payload.content;
      let theContent = this.thecontent;

      this.user = payload.user.name;
      let user = this.user;

      this.theMetaTitle = payload.metaTitle;
      let theMetaTitle = payload.metaTitle;

      this.theMetaDescription = payload.metaDescription;
      let theMetaDescription = payload.metaDescription;

      this.$emit("editBlog", {
        article: this.selectedBlog,
        user: user,
        content: theContent,
        metaTitle: theMetaTitle,
        metaDescription: theMetaDescription,
      });
    },
    removeBlog(index) {
      if (this.isConnected()) {
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
      }
    },
    unselect(index) {
      for (let i = 0; i < this.blogs.length; i++) {
        if (i != index) {
          let unselectBlog = document.getElementById("nouvBlog" + i);
          unselectBlog.style.backgroundColor = " rgb(75, 75, 75)";
        }
      }
    },
    open() {
      let myAdmin = document.getElementById("myAdmin");
      let myBlogs = document.getElementById("myBlogs");
      let editBlog = document.getElementById("editBlog");

      myBlogs.style.width = "40%";
      myAdmin.style.display = "flex";
      myAdmin.style.justifyContent = "space-around";
      editBlog.style.display = "block";
      editBlog.style.width = "55%";
    },
    openCreate() {
      if (this.isConnected()) {
        this.open();
        this.create = true;

        let blogContent = document.getElementById("blogContent");
        let blogTitle = document.getElementById("blogTitle");
        let blogMTitle = document.getElementById("blogMTitle");
        let blogMDescription = document.getElementById("blogMDescription");

        blogTitle.innerHTML = "";
        blogMTitle.value = "";
        blogMDescription.value = "";
        blogContent.value = "";

        blogTitle.style.display = "none";

        let blogTitleArea = document.getElementById("blogTitleArea");
        blogTitleArea.style.display = "block";
      }
    },
    openEdit(index) {
      if (this.isConnected()) {
        this.open();
        this.create = false;
        this.selectedBlog = index;
        let nouvBlog = document.getElementById("nouvBlog" + index);
        let blogContent = document.getElementById("blogContent");
        let blogTitle = document.getElementById("blogTitle");
        let blogMTitle = document.getElementById("blogMTitle");
        let blogMDescription = document.getElementById("blogMDescription");

        nouvBlog.style.backgroundColor = " rgb(121, 121, 121)";

        let blogTitleArea = document.getElementById("blogTitleArea");
        blogTitleArea.style.display = "none";

        blogTitle.style.display = "block";
        blogTitle.innerHTML = this.blogs[index].title;
        blogMTitle.value = this.blogs[index].metaTitle;
        blogMDescription.value = this.blogs[index].metaDescription;
        blogContent.value = this.blogs[index].content;

        this.unselect(index);

        return index;
      }
    },
  },
};
</script>

<style>
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

#createButton {
  border-radius: 10px;
  padding: 5px;
  margin: 10px;
}
#editButton {
  border-radius: 10px;
  padding: 5px;
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
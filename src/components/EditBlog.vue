<template>
  <div id="editBlog">
    <button id="xButton" v-on:click="closeEdit">X</button>
    <form action="" id="allInfos">
      <div id="metaInfos">
        <div id="baseInfos">
          <div class="baseMetas">
            <h2
              name=""
              cols="30"
              rows="1"
              id="blogTitle"
              style="display: none; color: #fff; text-decoration: underline"
            ></h2>
            <div id="blogTitleArea" style="display: none">
              <h4>Titre de l'article :</h4>
              <textarea
                cols="30"
                rows="1"
                id="blogTitleInput"
                required
              ></textarea>
              <p id="errorTitle" style="display: none; color: red">
                Un autre post a déjà ce titre
              </p>
            </div>
          </div>
          <br />
          <div class="baseMetas">
            <h4>Meta titre :</h4>
            <textarea
              name=""
              cols="30"
              rows="1"
              id="blogMTitle"
              required
            ></textarea>
          </div>
          <br />
          <div class="baseMetas">
            <h4>Meta description :</h4>
            <textarea
              name=""
              cols="30"
              rows="1"
              id="blogMDescription"
              required
            ></textarea>
          </div>
          <br />
        </div>
        <div id="imgBlog">
          <img
            src="./../assets/logo.png"
            style="width: 40px; height: 40px"
            alt=""
          />
          <h4>Modifier l'image</h4>
        </div>
      </div>
      <div>
        <h4>Corps du blog:</h4>
        <textarea
          name=""
          cols="40"
          rows="10"
          id="blogContent"
          required
        ></textarea>
      </div>
      <div v-if="create">
        <input
          type="submit"
          value="Valider la creation"
          v-on:click="sendCreation"
          class="validate"
          required
        />
      </div>
      <div v-else>
        <input
          type="submit"
          value="Valider les modifications"
          v-on:click="sendEdit"
          class="validate"
          required
        />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: ["index", "create", "theUser", "blogs"],

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
    newTime() {
      var date = new Date();
      let newDate =
        date.getDate() + "/" + (date.getMonth() + 1) + "/" + date.getFullYear();
      return newDate;
    },
    verifTitle(txt) {
      let index = 0;
      let blogLength = this.blogs.length;
      while (this.blogs[index].title != txt && index < blogLength - 1) {
        index++;
      }
      if (this.blogs[index].title == txt) {
        return true;
      } else {
        return false;
      }
    },

    sendCreation() {
      let blogContent = document.getElementById("blogContent").value;
      let blogTitle = document.getElementById("blogTitleInput").value;
      let blogMTitle = document.getElementById("blogMTitle").value;
      let blogMDescription = document.getElementById("blogMDescription").value;
      if (this.isConnected() && !this.verifTitle(blogTitle)) {
        if (
          blogContent != "" &&
          blogTitle != "" &&
          blogMTitle != "" &&
          blogMDescription != ""
        ) {
          this.newTime();
          this.closeEdit();

          this.$emit("sendCreation", {
            content: blogContent,
            title: blogTitle,
            metaTitle: blogMTitle,
            metaDescription: blogMDescription,
            user: this.theUser,
            date: this.newTime(),
          });
        }
      }
      if (this.verifTitle(blogTitle)) {
        document.getElementById("errorTitle").style.display = "block";
      }
    },
    sendEdit() {
      if (this.isConnected()) {
        let blogContent = document.getElementById("blogContent").value;
        let blogMTitle = document.getElementById("blogMTitle").value;
        let blogMDescription = document.getElementById("blogMDescription")
          .value;

        if (blogContent != "" && blogMTitle != "" && blogMDescription != "") {
          this.closeEdit();
          this.$emit("sendEdit", {
            content: blogContent,
            metaTitle: blogMTitle,
            metaDescription: blogMDescription,
            user: this.theUser,
          });
        }
      }
    },
    closeEdit() {
      let myBlogs = document.getElementById("myBlogs");
      myBlogs.style.width = "100%";
      let editBlog = document.getElementById("editBlog");
      editBlog.style.display = "none";

      let unselectBlog = document.getElementById("nouvBlog" + this.index);
      unselectBlog.style.backgroundColor = "rgb(75, 75, 75)";
    },
  },
};
</script>

<style>
.validate {
  border-radius: 10px;
  padding: 5px;
}
#editBlog {
  display: none;
  padding: 10px;
  background-color: rgb(146, 146, 146);
  position: relative;
}
#blogTitle,
#blogMTitle,
#blogMDescription,
#blogContent {
  overflow: hidden;
}
#xButton {
  position: absolute;
  right: 0;
  top: 0;
}
#metaInfos {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
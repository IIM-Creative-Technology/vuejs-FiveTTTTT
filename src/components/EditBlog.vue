<template>
  <div id="editBlog">
    <button id="xButton" v-on:click="closeEdit">X</button>
    <form action="" id="allInfos">
      <div id="metaInfos">
        <div id="baseInfos">
          <div class="baseMetas">
            <!-- <p>Titre du blog</p> -->
            <h2
              name=""
              cols="30"
              rows="1"
              id="blogTitle"
              style="display: none; color: #fff; text-decoration: underline"
            ></h2>
            <div id="blogTitleArea" style="display: none">
              <p>Titre de l'article</p>
              <textarea
                name=""
                cols="30"
                rows="1"
                id="blogTitleInput"
                required
              ></textarea>
            </div>

            <!-- <p style="display: none; color: red">Titre du blog</p> -->
          </div>
          <br />
          <div class="baseMetas">
            <p>Meta titre</p>
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
            <p>Meta description</p>
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
          <p>Modifier l'image</p>
        </div>
      </div>
      <div>
        <p>Corps du blog</p>
        <textarea
          name=""
          cols="40"
          rows="10"
          id="blogContent"
          required
        ></textarea>
      </div>
      <input
        type="submit"
        value="Valider la creation"
        v-if="create"
        v-on:click="sendCreation"
      />
      <input
        type="submit"
        value="Valider les modifications"
        v-else
        v-on:click="sendEdit"
      />
      <!-- v-on:click="sendEdit" -->
    </form>
  </div>
</template>

<script>
export default {
  props: ["index", "create", "theUser"],
  // data() {
  //   return {
  //     create: true,
  //   };
  // },

  methods: {
    newTime() {
      var date = new Date();
      let newDate =
        date.getDate() +
        "/" +
        (date.getMonth() + 1) +
        "/" +
        date.getFullYear();
      return newDate;
    },
    sendCreation() {
      this.closeEdit();
      this.newTime();
      let blogContent = document.getElementById("blogContent").value;
      // console.log("blogContent "+blogContent);
      let blogTitle = document.getElementById("blogTitleInput").value;
      // console.log("blogTitle "+blogTitle);
      let blogMTitle = document.getElementById("blogMTitle").value;
      let blogMDescription = document.getElementById("blogMDescription").value;

      this.$emit("sendCreation", {
        content: blogContent,
        title: blogTitle,
        metaTitle: blogMTitle,
        metaDescription: blogMDescription,
        user: this.theUser,
        date:this.newTime(),
      });
    },
    sendEdit() {
      this.closeEdit();

      // console.log(this.theUser);

      let blogContent = document.getElementById("blogContent").value;
      // let blogTitle = document.getElementById("blogTitle").value;
      let blogMTitle = document.getElementById("blogMTitle").value;
      let blogMDescription = document.getElementById("blogMDescription").value;

      // console.log("no");

      this.$emit("sendEdit", {
        content: blogContent,
        metaTitle: blogMTitle,
        metaDescription: blogMDescription,
        user: this.theUser,
      });
    },
    closeEdit() {
      let myBlogs = document.getElementById("myBlogs");
      myBlogs.style.width = "100%";
      let editBlog = document.getElementById("editBlog");
      editBlog.style.display = "none";
      // console.log("l'id " + this.index);

      let unselectBlog = document.getElementById("nouvBlog" + this.index);
      unselectBlog.style.backgroundColor = "rgb(75, 75, 75)";
    },
  },
};
</script>

<style>
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
/* #baseInfos .baseMetas {
  display: flex;
} */
#imgBlog {
}
</style>
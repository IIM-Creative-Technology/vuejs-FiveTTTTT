<template>
  <div id="myAdmin">
    <ul id="myBlogs">
      <li v-for="(blog, index) in blogs" :key="(blog, index)">
        <div id="nouvBlog">
          <p>{{ blog.theImages }}</p>
          <p>{{ blog.content }}</p>
          <div class="blogsActions">
            <button v-on:click="editeBlog(index)">Editer</button>
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
    <EditBlog />
  </div>
</template>

<script>
import EditBlog from "./EditBlog.vue";
export default {
  components: {
    EditBlog,
  },
  name: "Admin",
  data() {
    return {
      blogs: [
        { theImages: 1, content: "lorem" },
        { theImages: 2, content: "ipsum" },
      ],
    };
  },
  //   props: ["blogs"],
  methods: {
    removeBlog(index) {
      //   this.removerId = payload.removerId;
      //   let idCheck = this.removerId;
      let removeThisBlog = this.blogs;
      removeThisBlog.splice(index, 1);
    },
    editeBlog(index) {
      let myAdmin = document.getElementById("myAdmin");
      let myBlogs = document.getElementById("myBlogs");
      let theBlog = document.getElementById("editBlog");
      myBlogs.style.width = "40%";
      myAdmin.style.display = "flex";
      myAdmin.style.justifyContent = "space-between";
      theBlog.style.display = "block";
      theBlog.style.width = "40%";
      theBlog.innerHTML = this.blogs[index].content;
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
#nouvBlog {
  padding: 10px;
  border-radius: 10px;
  width: 80%;
  background-color: rgb(75, 75, 75);
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

#nouvBlog .blogsActions {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
<template>
  <div v-theme:column="'narrow'" id="show-blogs">
      <h1>博客总览</h1>
      <input type="text" placeholder="搜索" v-model="search">
      <div class="single-blog" v-for="(blog,index) in filteredBlogs" v-bind:key="index">
          <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
          <article>
              {{blog.body | snippet}}
          </article>
      </div>
  </div>
</template>

<script>
export default {
  name: 'show-blogs',
  data() {
      return {
        blogs: [],
        search: "",
      }
  },
  created () {
      //let url = "https://jsonplaceholder.typicode.com/posts";
      let url = "../../static/post.json";
      this.$http.get(url)
        .then(function(data) {
            this.blogs = data.body.slice(0, 10);
      })
  },
  computed: {
      filteredBlogs: function() {
          return this.blogs.filter((blog) => {
              return blog.title.match(this.search);
          })
      }
  },
  filters: {
      /* "to-uppercase":function(value) {
        return value.toUpperCase();
      } */
    toUppercase(value) {
      return value.toUpperCase();
    }
  },
  directives: {
    'rainbow': {
      bind(el, binding, vnode) {
        el.style.color = "#" + Math.random().toString(16).slice(2,8);
      }
    }
  }
}
</script>

<style>
#show-blogs {
    max-width: 800px;
    margin: 0 auto;
}

.single-blog {
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>

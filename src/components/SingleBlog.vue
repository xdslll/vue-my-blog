<template>
  <div id="single-blog">
    <h1>{{blog.title}}</h1>
    <article>{{blog.content}}</article>
    <p>作者：{{blog.author}}</p>
    <p>分类：</p>
    <ul>
      <li v-for="category in blog.categories" :key="category">
        {{category}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'single-blog',
  data () {
    return {
      id: this.$route.params.id,
      blog: {}
    }
  },
  created() {
    let url = "https://wd2653859633wrgdqg.wilddogio.com/posts/" + this.id + ".json";
    this.$http.get(url)
      .then(function(data) {
        console.log(data);
        this.blog = data.body;
      })
  }
}
</script>

<style scoped>
  #single-blog {
    max-width: 960px;
    margin: 0 auto;
    padding: 20px;
    background: #eee;
    border: 1px dotted #aaa;
  }
</style>

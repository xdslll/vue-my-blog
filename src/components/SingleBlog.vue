<template>
  <div id="single-blog">
    <h1>{{blog.title}}</h1>
    <article>{{blog.body}}</article>
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
    let url = "https://jsonplaceholder.typicode.com/posts/" + this.id;
    this.$http.get(url)
      .then(function(data) {
        //console.log(data);
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

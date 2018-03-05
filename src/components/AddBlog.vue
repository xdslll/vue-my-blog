<template>
  <div id="add-blog">
    <h2>写博客</h2>
    <form v-if="!isSubmitted">
        <label>主题</label>
        <input type="text" v-model="blog.title">
        <label>内容</label>
        <textarea v-model="blog.content"></textarea>
        <div id="checkboxes">
            <label>Vue.js</label>
            <input type="checkbox" v-model="blog.categories" value="Vue.js">
            <label>Node.js</label>
            <input type="checkbox" v-model="blog.categories" value="Node.js">
            <label>React.js</label>
            <input type="checkbox" v-model="blog.categories" value="React.js">
            <label>Angular4</label>
            <input type="checkbox" v-model="blog.categories" value="Angular4">
        </div>
        <label>作者</label>
        <select v-model="blog.author">
            <option v-bind:key="index" v-for="(author,index) in authors">{{author}}</option>
        </select>
        <button v-on:click.prevent="post">添加博客</button>
    </form>
    <h2 v-if="isSubmitted">博客添加成功</h2>
    <div id="preview">
        <h2>博客总览</h2>
        <h3>博客标题：{{blog.title}}</h3>
        <h3>博客内容：</h3>
        <p>{{blog.content}}</p>
        <h3>博客分类：</h3>
        <ul>
            <li v-bind:key="index" v-for="(category,index) in blog.categories">
                {{category}}
            </li>
        </ul>
        <h3>作者：</h3>
        <p>{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'add-blog',
  data () {
    return {
      blog: {
          title: "",
          content: "",
          categories: [],
          author: ""
      },
      authors: ["Sam", "Nicole", "Yoyo"],
      isSubmitted: false
    }
  },
  methods: {
      post: function() {
          let url = "https://wd2653859633wrgdqg.wilddogio.com/posts.json";
          this.$http.post(url, this.blog)
            .then(function(data){
              console.log(data);
              this.isSubmitted = true;
          });
      }
  }
}
</script>

<style scoped>
#add-blog * {
    box-sizing: border-box;
}

#add-blog {
    margin: 20px auto;
    max-width: 600px;
    padding: 20px;
}

label {
    display: block;
    margin: 20px 0 10px;
}

input[type="text"], textarea, select {
    display: block;
    width: 100%;
    padding: 8px;
}

textarea {
    height: 200px;
}

#checkboxes label {
    display: inline-block;
    margin-top: 0;
}

#checkboxes input {
    display: inline-block;
    margin-right: 10px;
}

#checkboxes {
    margin-top: 20px;
}

button {
    display: block;
    margin: 20px 0;
    background: crimson;
    color: #fff;
    border: 0;
    padding: 14px;
    border-radius: 4px;
    font-size: 18px;
    cursor: pointer;
}

#preview {
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}

h3 {
    margin-top: 10px;
}
</style>

<template>
  <div id="add-blog">
    <h2>添加博客</h2>
   <form v-if="!submited">
    <label>博客标题</label>
    <input type="text" v-model="blog.title">

    <label>博客内容</label>
    <textarea v-model="blog.content"></textarea>

    <div id="checkboxes">
      <label>Vue.js</label>
      <input type="checkbox" value="Vue.js" v-model="blog.categories">
      <label>Node.js</label>
      <input type="checkbox" value="Node.js" v-model="blog.categories">
      <label>React.js</label>
      <input type="checkbox" value="React.js" v-model="blog.categories">
      <label>Angular4.js</label>
      <input type="checkbox" value="Angular4.js" v-model="blog.categories">
    </div>
    <div>
      <label>作者</label>
      <select v-model="blog.author">
        <option v-for="author in authors">{{author}}</option>
      </select>
    </div>
   </form>

  <div v-if="submited">
    <h2>您的博客发布成功</h2>
  </div>
   <div id="preview">
     <h3>博客总览</h3>
     <p>博客标题: {{blog.title}}</p>
     <p>博客内容:</p>
     <p>{{blog.content}}</p>
     <p>博客分类:</p>
     <ul>
       <li v-for="(category,index) in blog.categories" :key="index">{{category}}</li>
     </ul>
     <p>作者： {{blog.author}}</p>
     <button v-on:click.prevent="postBlog">添加博客</button>
   </div>
  </div>
</template>

<script>
import Axios from 'axios'
export default {
  name: 'AddBlog',
  data () {
    return {
      blog: {
        title: '',
        content: '',
        categories: [],
        author:''
      },
      authors: ['mrokxu', 'qingfeng', 'guoqiong','zhangdan'],
      submited: false
    }
  },
  methods: {
    postBlog:function() {
      Axios.post('http://jsonplaceholder.typicode.com/posts', {
        title: this.blog.title,
        body: this.blog.content,
        userId: 1
      }).then((res)=>{
        console.log('res', res)
        this.submited = true
      }).catch(err=>{
        cosole.log('err', err)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
  input[type="text"], textarea,select {
    display: block;
    width: 100%;
    padding: 8px;
  }
  textarea {
    height: 200px;
  }
  
  
  #checkboxes {
    margin-top: 30px;
  }
  #checkboxes label {
    display: inline-block;
    margin-top: 0;
  }
   #checkboxes input {
    background: red;
    display:inline-block;
    margin-right: 10px;
   }
   button {
     display: block;
     margin: 20px 0;
     background: crimson;
     color: #fff;
     padding: 14px;
     border: 0;
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

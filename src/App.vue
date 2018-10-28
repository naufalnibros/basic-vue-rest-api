<template>
  <div>
    <form @submit.prevent="add">
      <input type="text" v-model="form.title"> <br>
      <textarea cols="30" rows="10" v-model="form.content"></textarea> <br>
      <button type="submit">SAVE</button>
    </form>
    <ul>
      <li v-for="article in articles" :key="article.id">
        {{ article.title }} <br>
        {{ article.content }} <br>
      </li>
    </ul>
    <button @click="load">LOAD DATA</button>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data(){
      return {
        form:{
          title: "",
          content: ""
        },
        articles:[]
      }
    }, 
    // mounted => data yang dipanggil ketika halaman dibuka
    // async mounted(){
    //   const response = await axios.get('http://localhost:3000/articles')
    //   this.articles = response.data
    // }
    mounted(){
    },

    methods :{
     async load(){
      const response = await axios.get('http://localhost:3000/articles')
      this.articles = response.data
     },
     async add(){
       try {
          const response = await axios.post('http://localhost:3000/articles', this.form)
          this.load()
          this.title = ""
          this.content = ""         
       } catch (error) {
        console.log(error);
       }
     } 
    }
  }
</script>
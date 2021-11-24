<template>
  <div class="home">

    <div class="nav">
          <h2 style="margin-left:5%"> Personal Blog</h2>


        <span class="mbutton" style="font-size:20px;cursor:pointer" @click="openNav">
  <button class="button"> <i class="fa fa-pencil"></i>Add Post</button></span>
    </div>
      <div id ="mobile" class="mobilenav">
      <a href="javascript:void(0)" class="closebtn" @click="closeNav">&times;</a>
      <div class="ml" >

        <div class='form'>

          <label>Write something</label>
          <br>
          <textarea type="text" v-model="Title" placeholder="Post Title"></textarea>
          <br>
          <textarea class="t"  v-model="Body" type="text" placeholder="Content"></textarea>
          <br>
          <button @click="addPost"> Submit </button>

        </div>

      </div>
  </div>


    




    <div style="text-align:center; font-size:20px; margin-top:2%"><p>Latest Posts</p></div>

    <div class="content">



      <div class="posts"  v-for="post in posts" :key="post._id"
    :id="post._id" :post="post">


     <router-link class="route" :to="'Post/' + post._id">
    <h1>{{ post.Title }}</h1>

    <p>{{ post.Body }}</p>
    <p>Contine reading.........</p>
     </router-link>
      </div>
    </div>
<!-----------------
    <div class="add">
      <div class="form">
        <input type="text" v-model="Title">
        <br>
        <textarea type="text" v-model="Body" ></textarea>
        <br>
        <button @click="addPost">Add</button>
      </div>
    </div>




  

    <div class="posts" v-for="post in posts" :key="post._id"
    :id="post._id" :post="post">


    <router-link :to="'Post/' + post._id">
    <div>
    {{ post.Title }}
    <p>Continue reading..........</p>
    </div>
    </router-link>

    </div> ----------->


  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'Home',
  data() {
    return{
      posts: []
    }
  },
  async created() {
    try {
      const response = await axios.get('https://blog-apiii.herokuapp.com/')
      this.posts = response.data
    }
    catch(err) {
      console.log(err)
    }
  },
  methods: {
    openNav() {
    document.getElementById("mobile").style.width = "100%";
},
closeNav() {
    document.getElementById("mobile").style.width = "0";
},
    async addPost(){
      const response = await axios.post('https://blog-apiii.herokuapp.com/',{
        Title: this.Title,
        Body: this.Body
      })
      this.posts = response.data
      location.reload()
    }
  }
}

</script>

<style scoped>
 h2{
   text-align: center;
   font-size: 30px;
 }
 p{

 }
 .content {
   width:100%;

   height:auto
 }
 .posts{
   width:40%;
   margin-left:30%;
   height:20vh;
   border:1px solid black;
   margin-top: 2%;
   border-radius:10px;
   margin-bottom:2%
 }
 .posts h1{
   margin-left:5%;
 }
 .posts p{
   overflow: hidden;
    white-space: nowrap;
  text-overflow: ellipsis;
  margin-left:2%
 }
 .route{
   text-decoration: none;;
   color:black;
 }
 .route:hover{
   color:steelblue
 }
 .mobilenav {

    height: 100%;
    width: 0;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
     background:#333b50;
    overflow-x: hidden;
    transition: 0.5s;
    padding-top: 60px;
}

.mobilenav a {
    padding: 2% 8px 8px 32px;
    text-decoration: none;
    font-size: 25px;
    font-weight: 550;
    color: black;
    display: block;
    transition: 0.3s;
}

.mobilenav a:hover {
    color: #f1f1f1;
}

.mobilenav .closebtn {
    position: absolute;
    top: 0;
    right: 25px;
    font-size: 36px;
    margin-left: 50px;
}
.mbutton{
  margin-left: 70%;
  display:flex;
  position:sticky;
  margin-top:1%;
}
.span{
  color:steelblue
}
.nav{
  display: flex;;
  background:steelblue;
  color:white
}
.form {
  width:50%;
  margin-left:25%;
  display:block;
}
.form button{
  width:25%;
  height:40px;
  background:steelblue;
  color:white;
  border:none;
}
label{
  color:white;
  font-size:20px
}
textarea{
  width:100%;
  resize: none;
}

.t{
  width:100%;
  margin-top:-2%;
  resize: none;
  height:60vh
}
.button{
  background: white;
  color:black;
  border:none;
  height:40px
}
@media screen and (max-width: 480px) {
  .posts{
    width:70%;
    margin-left:15%;
    height:25vh;
    margin-top:5%;
  }
  h2{
    font-size: 15px;;
  }
  .mbutton{
  margin-left: 65%;
  display:flex;
  font-size:15px !important;
  margin-top:1%;
  position:fixed;
  background:grey;
  color:white;
}
.form{
  width:90%;
  margin-left:5%
}
}


 
</style>
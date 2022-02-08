<template>
  <div class="home">

    <div class="nav">
          <h2 style="margin-left:5%"> Latest Posts</h2>


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


    





 




    <div class="contents">
      <div class="post" v-for="post in posts" :key="post._id"
    :id="post._id" :post="post">
        <h2>{{ post.Title }}<hr></h2>


        <p>{{ post.Body }}</p>





        <router-link :to="'Post/' + post._id"><button>Read More </button></router-link>
      </div>
    </div>


    


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
  background:teal;
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
  background:teal;
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
.contents{
  margin-top:5%;
  width:100%;
  display:inline-flex;
  flex-wrap: wrap;
}
.post{
  width:30%;
  margin-left:auto;
  margin-right:auto;
  border:1px solid teal;
  height:auto;
  border-radius:5%;

}
hr{
  width:3.25em
}
.post h2{
  font-weight: 900;
}
.post button{
  width:30%;
  border:1px solid teal;
  background: teal;;
  color:white;
  height:50px;
  margin-left:35%;
  margin-bottom:10px;
}
.post p{
  margin-top:10%;
  margin-bottom:15vh;
  width:80%;
  height: 150px;

  margin-left:10%;
  text-align: justify;
  font-size:18px;
  overflow: hidden;
  text-overflow: ellipsis; 
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
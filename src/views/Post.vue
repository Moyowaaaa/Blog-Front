<template>
    <div>

        <div class="nav">
            <router-link class="route" to="/"><p>Home</p></router-link>
        </div>
     
        <div class="content">
            <h2>{{ post.Title}}</h2>
            <br>
            <p>{{ post.Body }}</p>  




            <!----------------
        <h3>Comments</h3>

        <div v-for="comment in comments"
        :key="comment.id"
        :id="comment.id"
        :comment="comment">

        <h4>{{ comment.email }}</h4>
        <br>
        </div>----------->
        </div>
    </div>
</template>


<script>
import axios from 'axios'


export default {
    data() {
        return {
            post:[],
            comments:[],
        }
    },
    methods: {
        async getPost(id) {
            const response = await axios.get('https://blog-apiii.herokuapp.com/' + id)
            this.post = response.data
        }
    },
 
    mounted() {
        this.getPost(this.$route.params.id)   
    }
}
</script>

<style scoped>
.nav{
  display: flex;;
  background:steelblue;
  color:white;
  height:auto;
}
.nav p{
    padding-top:2%;
    font-size: 20px;
    padding-bottom: 2%;

}
.content{
    width:80%;
    margin-left:10%
}
.content h2{
    text-align: center;
    font-weight: 600;
}
.content p{
    font-size: 20px;
}


.route{
    color:white;
    margin-top:1%;
    margin-bottom:1%;
    font-size: 25px;
    margin-left:5%
}
.route:hover{
    text-decoration: none;
}
@media screen and (max-width: 480px) {
    .content p{
        text-align: justify;
    }
}

</style>
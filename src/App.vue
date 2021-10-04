<template>
  <h1>Add User</h1>
    <label for="unsername">Username:</label>
    <input type="text" id="username" v-model="newUser" @keyup.enter="addUser">
  <hr>
  <h1>Top score</h1>
    <div style="display: flex; justify-content: center;">
      <div class="user-card">
        <img src='./assets/photo.png'  :alt=topScorer.username>
        <div>
          <h2>{{ topScorer.username }}</h2>
          <br>
          <h2>Score: {{topScorer.score}}</h2>
        </div>
      </div>
    </div>
  <hr>
  <h1>Users</h1>
  <ul>
    <li v-for="user of users" :key="user.id">
      <div class="user-card">
        <img :src="user.image"  :alt="user.image">
        <div>
          <h2>{{ user.username }}</h2>
          <br>
          <h2>Score: {{user.score}}</h2>
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
import axios from 'axios';
const baseURL = "http://localhost:3000/users";


export default {
  name: 'App',
  components: {
  },
  data(){
    return {
      users: [],
      newUser: "",
      image: "./assets/photo.png",
      topScorer: {score: -1},
    }
  },
  methods: {
    async addUser(){
      const res = await axios.post(baseURL, {username: this.newUser, image: this.image, score: this.getScore()})
      this.users = [...this.users, res.data];
      this.newUser = "";
    },
    setTopScorer(users=this.users){
      users.forEach((user)=>{
        if(user.score > this.topScorer.score)
          this.topScorer = user;
      })
    },
    getScore(){
      return Math.floor(Math.random() * 101);
    },
    setScore(){
      const users = this.users.map((user)=>{
        if(user.score == null){
          const score = this.getScore();
          const updatedUser ={
            ...user, score
          }
          return updatedUser
        }        
        return user;
      });
      this.setTopScorer(users);
      this.users = users;
    }
  },
  async created() {
    try{
      const res = await axios.get(baseURL);
      this.users = res.data;
      this.setScore();
    }
    catch(e){
      console.error(e);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

li {
  list-style: none;
}

ul{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-content: center ;

}

.user-card {
  height: 200px;
  width: 500px;
  background-color: gray;
  margin: 10px;

  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-content: center;
}
.user-card img{
  max-height: 200px;
  max-width: 200px;

}
</style>

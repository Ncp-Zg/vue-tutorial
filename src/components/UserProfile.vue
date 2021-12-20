<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1>@{{ user.username }}</h1>
      <div class="user-profile_admin_badge" v-if="user.isAdmin">
      Admin
      </div>
      <div class="user-profile_follower_count">
        <strong>Followers : </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile_messages-wrapper">
      <div class="user-profile_messages">
        <Message v-for="message in user.messages" :key="message.id" :username="user.username" :message="message" @favourite="toggleFavourite"/>
      </div>
    </div>
  </div>
</template>

<script>
import Message from "./Message"

export default {
  name: "UserProfile",
  components:{
    Message
  },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_name",
        firstName: "name",
        lastName: "lastname",
        email: "name@g.com",
        isAdmin: false,
        messages:[
          {id:1,content:"deneme"},
          {id:2,content:"deneme2"}
        ]
      },
    };
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log("gained a follower");
      }
    },
  },

  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id){
      console.log(`favourited message ${id} `)
    }
  },
  mounted() {
    this.followUser();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}
.user-profile_user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}
.user-profile_admin_badge{
  background-color:purple;
  color:white;
  border-radius:5px;
  margin-right:auto;
  padding:0 10px;
  font-weight: bold;

}

.user-profile_messages{
  margin-right:15%
}
h1 {
  margin: 0;
}
a {
  color: #42b983;
}
</style>

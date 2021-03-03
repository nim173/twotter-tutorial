<template>
  <div>
    @{{ user.username}} - {{ fullName }}
    <br/>
    <div v-if="user.isAdmin">
      Admin
    </div>
    <!-- <div v-else>
      Not Admin
    </div> -->
    <strong>followers: {{ followers }}</strong>
    <br/>
    <button @click="followUser">Follow</button>
    <br/>
    <div>
      <TwootItem 
        v-for="twoot in user.twoots" 
        :key="twoot.id" 
        :username="user.username" 
        :twoot="twoot" 
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
  name: 'UserProfile',
  components: { TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'nim',
        firstName: 'Nimesh',
        lastName: 'Des',
        email: 'nchathuranga173@gmail.com',
        isAdmin: true,
        twoots: [
          { id:1, content: 'Twooter is amazing!' },
          { id:2, content: 'blah is amazing!' },
          { id:3, content: 'blahblah is amazing!' }
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log('Favourited Tweet: ', id);
    }
  },
  // lifecycle hook
  mounted() {
    this.followUser();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

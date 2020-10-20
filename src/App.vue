<template>
  <div class="centered">
    <img alt="Vue logo" src="./assets/logo.png">
  </div>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin </div>
      <div class="user-profile__followers-count">
        <strong>Followers:</strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__entry-wrapper">
      <!-- <div class="user-profile__entry" v-for="entry in user.entries" :key="entry.id"> 
      <!- - each for entry needs an id to be differentiated from the others, that is why the :key attribute is for - ->
        {{ entry.content }}
      </div>
      -->
      <EntryItem 
          v-for="entry in user.entries" 
          :key="entry.id" 
          :username="user.username" 
          :entry="entry" 
          @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>

<script>
import EntryItem from './components/EntryItem';

export default {
  name: 'App',
  components: { EntryItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: '_jorian1',
        firstName: 'Jorge',
        lastName: 'Rivera',
        email: 'jorge.rivera@ssde.com.mx',
        isAdmin: false,
        entries: [
          { id: 1, content: 'This is my first post!!!' },
          { id: 2, content: "Don't forget to subscribe to my channel SSDE!"},
          { id: 3, content: 'this is getting annoying...'},
          { id: 4, content: 'How many of this do I have to add?'},
          { id: 5, content: 'Yet another post'},
          { id: 6, content: 'So many thing to do...'},
          { id: 7, content: 'I wonder if this will see ht elight of day'}
        ]
      }
    }
  },
  watch: {
    followers(currVal, prevVal) {
      if( prevVal < currVal ) {
        console.log(`${this.user.username} has gained a follower`);
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
      this.followers ++;
    },
    toggleFavorite(id) {
      console.log(`Favorite entry: ${id}`);
    }
  },
  mounted(){ /** This runs after the component is loaded **/
    this.followUser();
  }
}
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  width: 350px;
  margin: auto;
}

.centered {
  text-align: center;
}

h1 {
  margin: 0;
}

.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
}

.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  font-weight: bold;
  margin-right: auto;
  padding: 0px 10px;
  border-radius: 5px;
}
</style>

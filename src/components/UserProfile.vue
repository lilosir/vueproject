<template>
  <div class="user-profile">
    <div class="user-profile-card">
      <h1 class="username">@{{ user.username }} - {{ fullName }}</h1>
      <div class="admin_tag" v-if="user.isAdmin">Admin</div>
      <strong>Followers: {{ followers }}</strong>
    </div>
    <div class="user-profile-tweets">
      <TweetItem
        v-for="t in user.tweets"
        :key="t.id"
        :username="user.username"
        :tweet="t"
        @favorite="triggerFavorite"
      />
    </div>
  </div>
</template>

<script>
import TweetItem from "./TweetItem";

export default {
  name: "UserProfile",
  components: { TweetItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "lilosir",
        firstName: "Oliver",
        lastName: "Sheng",
        email: "sryoliver@gmail.com",
        isAdmin: true,
        tweets: [
          { id: 1, content: "this is amazing" },
          { id: 2, content: "I love it" },
        ],
      },
    };
  },
  watch: {
    followers(newF) {
      if (newF === 5) {
        console.log("Yo, you got 5 followers");
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
    triggerFavorite(id) {
      console.log(`favoriate tweet ${id}`);
    },
  },
  mounted() {
    console.log("???");
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: flex;
}

.user-profile-card {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  align-self: flex-start;
}

.username {
  margin: 0px;
}

.admin_tag {
  display: flex;
  padding: 0px 10px;
  border-radius: 5px;
  background: purple;
  color: white;
  align-self: flex-start;
}

.user-profile-tweets {
  display: flex;
  flex: 1;
  flex-direction: column;
}
</style>
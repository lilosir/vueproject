<template>
  <div class='tweet-item' @click="favoriteTweet(tweet.id)">
    <div class='tweet-name'>@{{ username }}</div>
    <div>{{ tweet.content }}</div>
  </div>
</template>

<script>
export default {
  name: "TweetItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    tweet: {
      type: Object,
      required: true,
    },
  },
  methods: {
    favoriteTweet(id) {
      this.$emit('favorite', id)
    }
  }
};
</script>

<style>
.tweet-item {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  margin-bottom: 20px;
  cursor: pointer;
  transition: all 0.25s ease;
}

.tweet-item:hover {
  transform: scale(1.1, 1.1);
}

.tweet-name {
  font-weight: bold;
}
</style>
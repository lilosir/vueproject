<template>
  <form
    class="user-profile-create-tweet"
    @submit.prevent="createNewTweet"
    :class="{ exceeded: state.tweetContentCharacterCount > 180 }"
  >
    <label for="newTweet">
      <strong>New Tweet</strong>
      ({{ state.tweetContentCharacterCount }}/180)
    </label>
    <textarea id="newTweet" rows="4" v-model="state.tweetContent" />

    <div class="user-profile-create-tweet-type">
      <label for="newTweet"><strong>Type: </strong></label>
      <select id="tweetTypes" v-model="state.tweetType">
        <option v-for="(tt, i) in state.tweetTypes" :value="tt.value" :key="i">
          {{ tt.name }}
        </option>
      </select>
    </div>

    <button>Tweet!</button>
  </form>
</template>

<script>
import { computed, reactive } from "vue";

export default {
  props: {},
  setup(props, ctx) {
    const state = reactive({
      tweetTypes: [
        { id: 1, value: "draft", name: "Draft" },
        { id: 2, value: "instant", name: "Instant Tweet" },
      ],
      tweetContent: "",
      tweetType: "instant",
      tweetContentCharacterCount: computed(() => state.tweetContent.length),
    });

    const createNewTweet = () => {
      if (
        state.tweetContent &&
        state.tweetContentCharacterCount <= 180 &&
        state.tweetType !== "draft"
      ) {
        ctx.emit("add-tweet", state.tweetContent);
        state.tweetContent = "";
      }
    };

    return {
      state,
      createNewTweet,
    };
  },
  name: "CreateTweetPanel",
};
</script>

<style lang='scss' scoped>
.user-profile-create-tweet {
  padding-top: 20px;
  display: flex;
  flex-direction: column;

  &.exceeded {
    color: red;
    border-color: red;

    button {
      background-color: red;
      border: none;
      color: white;
    }
  }
}
</style>
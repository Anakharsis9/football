<template>
  <div class="matchTable_wrapper">
    <h2>List of matches</h2>
    <ul>
      <li v-for="(match, index) in getSortedPlayedMatches" :key="index">
        <span>{{ match.teams }}</span>
        <span>{{ match.score }}</span>
        <span>{{ match.date }}</span>
        <hr />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MatchTable",
  props: {
    playedMatches: Array,
  },
  computed: {
    getSortedPlayedMatches() {
      return [...this.playedMatches].reverse();
    },
  },
};
</script>

<style lang="css" scoped>
.matchTable_wrapper {
  height: 25%;
  margin-top: 10px;
  padding: 10px;
  border: 1px solid gray;
  overflow-y: scroll;
  display: flex;
  flex-direction: column;
  align-items: center;
}

ul {
  width: 100%;
  margin-top: 5px;
  list-style: none;
}

li {
  width: 100%;
  margin-bottom: 10px;
  display: grid;
}
</style>

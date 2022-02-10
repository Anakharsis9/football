<template>
  <div class="topTeamsTable_wrapper">
    <h2>TOP 3</h2>
    <ol>
      <li v-for="(team, index) in getTopTeams" :key="index">
        {{ index + 1 }}. {{ team.name }} wins:{{ team.count }}
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "TopTeamsTable",
  props: {
    playedMatches: Array,
    teamsList: Array,
  },
  data: () => ({}),
  computed: {
    teamsStat() {
      const winners = this.playedMatches
        .map((match) => match.winnerId)
        .reduce((map, winnerId) => {
          map[winnerId] = map[winnerId] ? map[winnerId] + 1 : 1;
          return map;
        }, {});

      return winners;
    },
    getTopTeams() {
      const unordered = [];
      for (const id in this.teamsStat) {
        if (id !== "null") {
          unordered.push({
            name: this.findByTeamId(id).name,
            count: this.teamsStat[id],
          });
        }
      }
      return unordered.sort((a, b) => a.count - b.count).slice(0, 3);
    },
  },
  methods: {
    findByTeamId(id) {
      return this.teamsList.find((team) => team.id === id) || "not found";
    },
  },
};
</script>

<style lang="css" scoped>
.topTeamsTable_wrapper {
  height: 25%;
  margin-top: 10px;
  padding: 10px;
  border: 1px solid gray;
  overflow-y: scroll;
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* ul {
  width: 100%;
  margin-top: 5px;
  list-style: none;
} */

li {
  width: 100%;
  margin-bottom: 10px;
  display: grid;
}
</style>

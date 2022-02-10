<template>
  <div id="app">
    <Field
      @getMatchInfo="playedMatches.push($event)"
      :teamsList="teamsList"
      class="field"
    ></Field>
    <info-tables
      @teamsListUpdate="teamsList = $event"
      :teamsList="teamsList"
      :playedMatches="playedMatches"
      class="infoTables"
    ></info-tables>
  </div>
</template>

<script>
import Field from "@/components/Field.vue";
import InfoTables from "@/components/InfoTables.vue";

export default {
  name: "App",
  components: {
    Field,
    InfoTables,
  },
  data: () => ({
    teamsList: [],
    playedMatches: [
      {
        winner: "Team Spirit",
        winnerId: "team_4907.978554096723",
        score: "4:0",
        date: "3/2/2022 16:46",
        teams: "Team Spirit vs DreAM Team",
        teamsIds: ["team_4907.978554096723", "team_7953.730122914287"],
      },
      {
        winner: "DreAM Team",
        winnerId: "team_7953.730122914287",
        score: "7:18",
        date: "3/2/2022 16:46",
        teams: "Team 1 vs DreAM Team",
        teamsIds: ["team_5714.88511895963", "team_7953.730122914287"],
      },
    ],
  }),
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  outline: none;
  font-family: "Courier New", Courier, monospace;
}
#app {
  padding: 20px;
  overflow-x: hidden;
  display: grid;
  gap: 10px;
  grid-template-columns: 2fr 1fr;
  height: 100vh;
}

.addBtn {
  width: 180px;
  height: 40px;
  border: none;
  font-size: 18px;
  color: white;
  background-color: rgb(52, 67, 202);
  margin-top: 5px;
}
</style>

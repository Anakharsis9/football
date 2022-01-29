<template>
  <div class="wrapper">
    <match-settings :teamsList="teamsList"></match-settings>
    <div class="field_container">
      <div class="team team1">
        <div class="player player1"></div>
        <div class="player player2"></div>
        <div class="player player3"></div>
        <div class="player player4"></div>
        <div class="player player5"></div>
        <div class="player player6"></div>
      </div>
      <div class="team team2">
        <div class="player player1"></div>
        <div class="player player2"></div>
        <div class="player player3"></div>
        <div class="player player4"></div>
        <div class="player player5"></div>
        <div class="player player6"></div>
      </div>
    </div>
  </div>
</template>

<script>
import MatchSettings from "@/components/MatchSettings.vue";

export default {
  name: "Field",
  props: {
    teamsList: {
      type: Array,
    },
  },
  components: {
    MatchSettings,
  },
  data: () => ({}),
};
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
}

.field_container {
  background-image: url("../assets/Field.svg");
  background-size: contain;
  background-repeat: no-repeat;
  width: 1000px;
  height: 750px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-content: center;
  align-items: center;
}

.team {
  margin-top: -50px;
  display: grid;
  width: 80%;
  height: 65%;
  grid-template: repeat(5, 1fr) / repeat(4, 1fr);
  justify-items: center;
  align-items: center;
}
.team1 {
  margin-left: 95px;
}
.team1 > .player {
  width: 50px;
  height: 50px;
  border: 2px solid red;
}
.team1 > .player1 {
  grid-column: 2/3;
}
.team1 > .player2 {
  grid-column: 4/5;
}
.team1 > .player3 {
  grid-row: 3/4;
}
.team1 > .player4 {
  grid-row: 3/4;
  grid-column: 3/4;
}
.team1 > .player5{
  grid-row: 5/6;
  grid-column: 2/3;
}
.team1 > .player6{
  grid-row: 5/6;
  grid-column: 4/5;
}


.team2 > .player1 {
  grid-column: 2/3;
}
.team2 > .player2 {
  grid-row: 2/3;
  grid-column: 3/4;
}
.team2 > .player3 {
  grid-row: 3/4;
  
}
.team2 > .player4 {
  grid-row: 3/4;
  grid-column: 4/5;
}
.team2 > .player5{
  grid-row: 4/5;
  grid-column: 3/4;
}
.team2 > .player6{
  grid-row: 5/6;
  grid-column: 2/3;
}
.team2 {
}

.team2 > .player {
  width: 50px;
  height: 50px;
  border: 2px solid blue;
}
</style>

<template>
  <div class="field_wrapper">
    <match-settings
      :isGameOver="isGameOver"
      :teamsList="teamsList"
      @settingModeChange="isSettingMode = $event"
      @twoTeams="twoTeams = $event"
      @startMatch="startMatch"
      @offGameOver="isGameOver = $event"
      @randomPlayersPlace="randomPlayersPlace"
    ></match-settings>
    <div class="field_container">
      <cells
        @getTeamDist="redTeamDist = $event"
        :team="twoTeams[0]"
        :isRandomPlayersPlace="isRandomPlayersPlace"
        v-if="isSettingMode"
        class="team team1"
      >
      </cells>
      <cells
        @getTeamDist="blueTeamDist = $event"
        :team="twoTeams[1]"
        :isRandomPlayersPlace="isRandomPlayersPlace"
        v-if="isSettingMode"
        class="team team2"
      >
      </cells>
    </div>
  </div>
</template>

<script>
import MatchSettings from "@/components/MatchSettings.vue";
import Cells from "@/components/Cells.vue";

export default {
  name: "Field",
  props: {
    teamsList: {
      type: Array,
    },
  },
  components: {
    MatchSettings,
    Cells,
  },
  data: () => ({
    isSettingMode: false,
    isRandomPlayersPlace: 0,
    twoTeams: [],
    redTeamDist: null,
    blueTeamDist: null,
    isGameOver: false,
    matchInfo: null,
    matchWinner: null,
    score: null,
  }),
  methods: {
    randomPlayersPlace() {
      this.isRandomPlayersPlace++;
    },
    startMatch() {
      if (
        this.checkTeamDist(this.redTeamDist) &&
        this.checkTeamDist(this.blueTeamDist)
      ) {
        const score1 = Math.floor(Math.random() * 20);
        const score2 = Math.floor(Math.random() * 20);
        
        const winner = score1 > score2 ? 0 : score1 === score2 ? "tie" : 1;
        alert("The match started. There is a hot game going on");
        const d = new Date();
        const date = `${d.getDate()}/${
          d.getMonth() + 1
        }/${d.getFullYear()} ${d.getHours()}:${d.getMinutes()}`;
        const whoPlayed = `${this.twoTeams[0].name} vs ${this.twoTeams[1].name}`;
        const whoPlayedIds = [this.twoTeams[0].id, this.twoTeams[1].id];

        this.score = `${score1}:${score2}`;
        if (winner === "tie") {
          alert(
            `It's tie match! In the match ${whoPlayed} winner is nobody! Score is ${this.score}`
          );
          this.matchInfo = {
            winner: null,
            winnerId: null,
            score: this.score,
            date: date,
            teams: whoPlayed,
            teamsIds: whoPlayedIds,
          };
        } else {
          this.matchWinner = this.twoTeams[winner];

          alert(
            `In the match ${whoPlayed} winner is ${this.matchWinner.name}! Score is ${this.score}`
          );
          this.matchInfo = {
            winner: this.matchWinner.name,
            winnerId: this.matchWinner.id,
            score: this.score,
            date: date,
            teams: whoPlayed,
            teamsIds: whoPlayedIds,
          };
        }
        this.$emit("getMatchInfo", this.matchInfo);
        this.isGameOver = true;
      } else alert("Select players for both teams");
    },
    checkTeamDist(teamDist) {
      return !Object.values(teamDist).includes(-1);
    },
  },
};
</script>

<style lang="scss" scoped>
.field_wrapper {
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
</style>

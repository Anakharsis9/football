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
  }),
  methods: {
    randomPlayersPlace() {
      this.isRandomPlayersPlace++;
    },
    startMatch() {
      const isTeamsFull =
        this.checkTeamDist(this.redTeamDist) &&
        this.checkTeamDist(this.blueTeamDist);
      if (!isTeamsFull) return alert("Select players for both teams");

      alert("The match started. There is a hot game going on");

      const score1 = Math.floor(Math.random() * 20);
      const score2 = Math.floor(Math.random() * 20);
      const winner = score1 > score2 ? 0 : score1 === score2 ? "tie" : 1;
      const score = `${score1}:${score2}`;

      const d = new Date();
      const date = `${d.getDate()}/${
        d.getMonth() + 1
      }/${d.getFullYear()} ${d.getHours()}:${d.getMinutes()}`;

      const whoPlayed = `${this.twoTeams[0].name} vs ${this.twoTeams[1].name}`;
      const whoPlayedIds = [this.twoTeams[0].id, this.twoTeams[1].id];

      const matchInfo = {
        winner: null,
        winnerId: null,
        score,
        date,
        teams: whoPlayed,
        teamsIds: whoPlayedIds,
      };
      if (winner === "tie") {
        alert(
          `It's tie match! In the match ${whoPlayed} winner is nobody! Score is ${score}`
        );
      } else {
        const matchWinner = this.twoTeams[winner];

        alert(
          `In the match ${whoPlayed} winner is ${matchWinner.name}! Score is ${score}`
        );
        matchInfo.winner = matchWinner.name;
        matchInfo.winnerId = matchWinner.id;
      }

      this.$emit("getMatchInfo", matchInfo);
      this.isGameOver = true;
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

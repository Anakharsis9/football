<template>
  <div class="field_wrapper">
    <match-settings
      :isGameOver="isGameOver"
      :teamsList="teamsList"
      @settingModeChange="isSettingMode = $event"
      @twoTeams="twoTeams = $event"
      @startMatch="startMatch"
      @offGameOver="isGameOver = $event"
    ></match-settings>
    <div class="field_container">
      <cells
        @getTeamDist="redTeamDist = $event"
        :team="twoTeams[0]"
        v-if="isSettingMode"
        class="team team1"
      >
      </cells>
      <cells
        @getTeamDist="blueTeamDist = $event"
        :team="twoTeams[1]"
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
    twoTeams: [],
    redTeamDist: null,
    blueTeamDist: null,
    isGameOver: false,
    matchWinner: null,
  }),
  methods: {
    startMatch() {
      if (
        this.checkTeamDist(this.redTeamDist) &&
        this.checkTeamDist(this.blueTeamDist)
      ) {
        const winner = Math.floor(Math.random() * 2);
        alert("The match started. There is a hot game going on");
        this.matchWinner = this.twoTeams[winner];
        alert(`The winner is ${this.matchWinner.name}!`);
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

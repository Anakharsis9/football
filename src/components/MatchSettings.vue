<template>
  <div class="setting_wrapper">
    <div class="team">
      <span class="label"> First Team: </span>
      <h3>{{ team1.name || "Team name" }}</h3>
      <ul class="list">
        <li
          v-for="(player, index) in team1.players"
          :key="index"
          class="player_li_red"
        >
          {{ player.number }} {{ player.fullName }}
        </li>
      </ul>
    </div>
    <div class="buttons">
      <button class="addBtn" v-if="!isSettingMode" @click="settingMatch">
        Match Settings
      </button>
      <button class="addBtn" v-if="isSettingMode" @click="exitSettings">
        Exit
      </button>
      <button class="addBtn" v-if="isSettingMode" @click="startMatch">
        Start Match
      </button>
      <button class="addBtn" v-if="isSettingMode" @click="randomPlayersPlace">
        Random players place
      </button>
    </div>
    <div class="team">
      <span class="label"> Second Team: </span>
      <h3>{{ team2.name || "Team name" }}</h3>
      <ul class="list">
        <li
          v-for="(player, index) in team2.players"
          :key="index"
          class="player_li_blue"
        >
          {{ player.number }} {{ player.fullName }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { getRandom } from "@/utils";

export default {
  name: "MatchSettings",
  props: {
    teamsList: Array,
    isGameOver: Boolean,
  },
  data: () => ({
    isSettingMode: false,
    team1: {},
    team2: {},
  }),
  methods: {
    settingMatch() {
      this.isSettingMode = true;

      const validTeams = this.teamsList.filter((t) => t.players.length > 5);
      const len = validTeams.length;

      const random = getRandom(len);
      this.team1 = validTeams[random];

      let random2 = getRandom(len);
      while (random2 === random) {
        random2 = getRandom(len);
      }

      this.team2 = validTeams[random2];

      this.$emit("twoTeams", [this.team1, this.team2]);
      this.$emit("offGameOver", false);
    },
    exitSettings() {
      this.team1 = {};
      this.team2 = {};
      this.isSettingMode = false;
    },
    startMatch() {
      this.$emit("startMatch");
    },

    randomPlayersPlace() {
      this.$emit("randomPlayersPlace");
    },
  },

  watch: {
    isSettingMode: function (newVal) {
      this.$emit("settingModeChange", newVal);
    },
    isGameOver: function (newValue) {
      if (newValue) this.exitSettings();
    },
  },
};
</script>

<style>
.setting_wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  margin-bottom: 20px;
}
.list {
  height: 130px;
  overflow-y: scroll;
  margin-top: 10px;
  margin-bottom: 10px;
}
.buttons {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.player_li_red {
  border: 2px solid red;
  margin-bottom: 5px;
}
.player_li_blue {
  border: 2px solid blue;
  margin-bottom: 5px;
}
</style>

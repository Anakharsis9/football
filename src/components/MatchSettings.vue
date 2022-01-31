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
      <button class="addBtn" v-if="isSettingMode">Start Match</button>
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
export default {
  name: "MatchSettings",
  props: {
    teamsList: Array,
    selectedCell: {
      type: Object,
      required: false,
    },
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
      const random = this.getRandom(len);
      this.team1 = validTeams[random];
      let random2 = this.getRandom(len);
      while (random2 === random) {
        random2 = this.getRandom(len);
      }
      this.team2 = validTeams[random2];
      this.$emit("twoTeams", [this.team1, this.team2]);
    },
    exitSettings() {
      this.team1 = {};
      this.team2 = {};
      this.isSettingMode = false;
    },
    getRandom(length) {
      return Math.floor(Math.random() * length);
    },
  },
  watch: {
    isSettingMode: function (newVal) {
      this.$emit("settingModeChange", newVal);
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

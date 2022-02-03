<template>
  <div>
    <div
      v-for="(n, index) in 6"
      :key="n"
      class="player"
      :class="{
        ['player' + n]: true,
      }"
    >
      <select
        @change="updateCell(index, +$event.target.value)"
        class="player_select"
      >
        <option :value="-1">-</option>
        <option
          v-for="player in filterPlayerOptions(teamDist[index])"
          :value="player.number"
          :key="player.number"
        >
          {{ player.number + " " + player.fullName }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cells",
  props: { team: { type: Object, require: true } },
  data: () => ({
    teamDist: { 0: -1, 1: -1, 2: -1, 3: -1, 4: -1, 5: -1 },
  }),
  methods: {
    filterPlayerOptions(currentPlayerNumber) {
      const chosenPlayers = Object.values(this.teamDist).filter(
        (number) => currentPlayerNumber !== number
      );
      return this.team.players.filter(
        (player) => !chosenPlayers.includes(player.number)
      );
    },
    updateCell(index, value) {
      this.teamDist[index] = value;
    },
    onTeamDistUpdate(newVal) {
      this.$emit("getTeamDist", newVal);
    },
  },
  watch: {
    teamDist: "onTeamDistUpdate",
  },
  created() {
    this.onTeamDistUpdate(this.teamDist);
  },
};
</script>

<style>
.player_select {
  width: 100px;
}

.player {
  background-color: rgba(0, 0, 0, 0.2);
  width: 100px;
  height: 50px;
}
.team > .player:hover {
  border: 2px solid yellow;
}

.team1 > .player {
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
.team1 > .player5 {
  grid-row: 5/6;
  grid-column: 2/3;
}
.team1 > .player6 {
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
.team2 > .player5 {
  grid-row: 4/5;
  grid-column: 3/4;
}
.team2 > .player6 {
  grid-row: 5/6;
  grid-column: 2/3;
}

.team2 > .player {
  border: 2px solid blue;
}
</style>

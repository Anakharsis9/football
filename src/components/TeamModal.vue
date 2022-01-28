<template>
  <div class="modal_wrapper" ref="modal_wrapper">
    <div class="modal">
      <div class="modal_header">
        <h2>Team</h2>
        <fas class="close" icon="times" @click="closeModal" />
      </div>
      <div class="modal_content">
        <div class="team_info">
          <span>Team name:</span>
          <input v-model="name" type="text" placeholder="Team name" />
          <h4>Players:</h4>
          <ul class="list">
            <li v-for="(player, index) in players" :key="index">
              <div class="li_content">
                {{ player.number }} {{ player.fullName }}
                <player-edit
                  :player="player"
                  :numbers="players.map((pl) => pl.number)"
                ></player-edit>
                <fas
                  @click.stop="deletePlayer(player)"
                  class="close"
                  icon="times"
                />
              </div>
            </li>
          </ul>
        </div>
        <div class="player_creation">
          <h3>New player</h3>
          <div class="player_inp">
            <span>Player fullname:</span>
            <input
              v-model="playerName"
              type="text"
              placeholder="Player fullname"
            />
          </div>
          <div class="player_inp">
            <span>Player number:</span>
            <input
              v-model.number="playerNumber"
              type="number"
              placeholder="Player number"
            />
            <span class="error" v-if="playerError">
              Player with {{ playerNumber }} number exist. Please, choose
              another number.
            </span>
          </div>
          <button @click="addPlayer" class="addBtn">Add player</button>
        </div>
      </div>
      <div class="modal_footer">
        <button v-if="isNewTeam" @click="addTeam" class="addBtn">
          Add Team
        </button>
        <button v-else @click="updateTeam" class="addBtn">Update Team</button>
      </div>
    </div>
  </div>
</template>

<script>
import PlayerEdit from "@/components/PlayerEdit.vue";
export default {
  name: "TeamModal",
  components: {
    PlayerEdit,
  },
  props: {
    team: {
      type: Object,
      required: false,
    },
  },
  data: () => ({
    name: "",
    players: [],
    playerName: "",
    playerNumber: null,
  }),

  methods: {
    closeModal() {
      this.name = "";
      this.players = [];
      this.playerName = "";
      this.playerNumber = null;
      this.$emit("closeModal");
    },
    addPlayer() {
      if (
        !this.playerError &&
        this.playerName.length !== 0 &&
        this.playerNumber !== null
      ) {
        this.players.push({
          fullName: this.playerName,
          number: this.playerNumber,
        });
      }
      this.playerName = "";
      this.playerNumber = null;
    },
    addTeam() {
      if (this.name.length === 0) return;
      this.$emit("addTeam", {
        id: `team_${Math.random() * 10000}`,
        name: this.name,
        players: this.players,
      });
      this.closeModal();
    },
    updateTeam() {
      this.$emit("updateTeam", {
        id: this.team.id,
        name: this.name,
        players: this.players,
      });

      this.closeModal();
    },
    deletePlayer(player) {
      this.players = this.players.filter((p) => p.number !== player.number);
    },
  },
  computed: {
    isNewTeam() {
      return !this.team;
    },
    playerError() {
      return this.players.find((p) => p.number === this.playerNumber);
    },
  },
  created() {
    if (!this.isNewTeam) {
      this.name = this.team.name;
      this.players = JSON.parse(JSON.stringify(this.team.players));
    }
  },
  mounted() {
    let vm = this;
    document.addEventListener("click", (item) => {
      if (item.target === vm.$refs["modal_wrapper"]) {
        vm.closeModal();
      }
    });
  },
};
</script>

<style scoped>
.modal_wrapper {
  width: 100vw;
  height: 100vh;
  position: absolute;
  background-color: rgba(64, 64, 64, 0.6);
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal {
  top: 20%;
  position: fixed;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  width: 800px;
  height: 500px;
  z-index: 10;
  background-color: white;
  box-shadow: 0 0 17px 0 #e7e7e7;
}
.modal_header {
  width: 100%;
  display: grid;
  grid-template: auto/99% 1fr;
  font-size: 20px;
  justify-content: center;
  align-items: center;
}
h2 {
  justify-self: center;
}
.close {
  justify-self: end;
}

.modal_content {
  margin-top: 20px;
  height: 80%;
  width: 100%;
  display: grid;
  grid-template: auto/1fr 1fr;
  gap: 10px 80px;
}
input {
  width: 180px;
  font-size: 18px;
}
.team_info {
  display: flex;
  flex-direction: column;
  padding-left: 20px;
}
h4 {
  margin-top: 20px;
}
.player_creation {
  display: flex;
  flex-direction: column;
}
.player_inp {
  margin-top: 10px;
  display: flex;
  flex-direction: column;
}
.error {
  color: red;
}
</style>

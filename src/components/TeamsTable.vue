<template>
  <div class="wrapper">
    <team-modal
      v-if="isModalVisible"
      :team="chosenTeam"
      @closeModal="closeModal"
      @addTeam="addTeam"
      @updateTeam="updateTeam"
    >
    </team-modal>
    <div class="container">
      <h2>Teams</h2>
      <ul class="list">
        <li
          v-for="team in teamsList"
          :key="team.id"
          class="teamItem"
          @click="openCreateModal(team)"
        >
          {{ team.name }}
          <fas @click.stop="deleteTeam(team)" class="close" icon="times" />
        </li>
      </ul>
    </div>
    <button class="addBtn" @click="openCreateModal(null)">Create Team</button>
  </div>
</template>

<script>
import TeamModal from "@/components/TeamModal.vue";

export default {
  name: "TeamsTable",
  components: {
    TeamModal,
  },
  data: () => ({
    teamsList: [
      {
        id: "team_5714.88511895963",
        name: "Team 1",
        players: [
          { pId: "player_1234.88511895963", fullName: "Awww Vkmk", number: 12 },
          { pId: "player_5079.603139551001", fullName: "Ankjs", number: 121 },
          { pId: "player_1731.4797619485023", fullName: "Lorem", number: 14 },
          { pId: "player_6860.281237261332", fullName: "Wdsaq", number: 16 },
          { pId: "player_1765.1816410384247", fullName: "ACddv", number: 134 },
          { pId: "player_2771.870812179851", fullName: "aDVvd", number: 17 },
        ],
      },
      {
        id: "team_4907.978554096723",
        name: "Team Spirit",
        players: [
          { pId: "player_3019.877253859979", fullName: "awd", number: 122 },
          { pId: "player_9332.418508944786", fullName: "addwd", number: 15 },
          { pId: "player_1675.3513052416947", fullName: "JBSC", number: 17 },
          { pId: "player_8397.144167620434", fullName: "awdwd", number: 16 },
          { pId: "player_2579.7626288629117", fullName: "awraga", number: 173 },
          { pId: "player_9349.552968711645", fullName: "wffw", number: 153 },
        ],
      },
      {
        id: "team_7953.730122914287",
        name: "DreAM Team",
        players: [
          { pId: "player_4903.82238553819", fullName: "Ansar", number: 65 },
          { pId: "player_7002.410107192418", fullName: "Gay", number: 223 },
          { pId: "player_8157.395264705049", fullName: "FullHd", number: 32 },
          { pId: "player_8273.318635083631", fullName: "Kambala", number: 14 },
          { pId: "player_990.1906282376283", fullName: "Kira", number: 90 },
          { pId: "player_7312.051587022308", fullName: "Juni", number: 30 },
        ],
      },
    ],

    isModalVisible: false,
    chosenTeam: null,
  }),
  methods: {
    openCreateModal(team = null) {
      this.isModalVisible = true;
      this.chosenTeam = team;
    },
    closeModal() {
      this.isModalVisible = false;
      this.chosenTeam = null;
    },
    addTeam(newTeam) {
      this.teamsList.push(newTeam);
    },
    updateTeam(team) {
      this.teamsList = this.teamsList.map((t) => {
        if (t.id === team.id) return team;
        return t;
      });
    },
    deleteTeam(team) {
      this.teamsList = this.teamsList.filter((t) => t.id !== team.id);
    },
    onTeamsListUpdate(newValue) {
      this.$emit("teamsListUpdate", newValue);
    },
  },
  watch: {
    teamsList: "onTeamsListUpdate",
  },
  created() {
    this.onTeamsListUpdate(this.teamsList);
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  height: 40%;
  border: 1px solid gray;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-direction: column;
  padding-top: 10px;
  padding-bottom: 10px;
}
.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
.list {
  padding-top: 20px;
  font-size: 18px;
  height: 250px;
  overflow-y: scroll;
}
.teamItem {
  border-bottom: 1px solid rgb(52, 67, 202);
}
.teamItem:hover {
  color: rgb(52, 67, 202);
}
</style>

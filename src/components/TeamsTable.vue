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
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  height: 50%;
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
}
.teamItem {
  border-bottom: 1px solid rgb(52, 67, 202);
}
.teamItem:hover {
  color: rgb(52, 67, 202);
}
</style>

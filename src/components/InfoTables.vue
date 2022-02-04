<template>
  <div class="wrapper">
    <teams-table
      @teamsListUpdate="$emit('teamsListUpdate', $event)"
    ></teams-table>
    <match-table :playedMatches="playedMatches"></match-table>
    <top-teams-table
      :teamsList="teamsList"
      :playedMatches="playedMatches"
    ></top-teams-table>
  </div>
</template>

<script>
import TeamsTable from "@/components/TeamsTable.vue";
import MatchTable from "@/components/MatchTable.vue";
import TopTeamsTable from "@/components/TopTeamsTable.vue";

export default {
  name: "InfoTables",
  props: {
    playedMatches: Array,
    teamsList: Array,
  },
  components: {
    TeamsTable,
    MatchTable,
    TopTeamsTable,
  },
  data: () => ({}),
};
</script>

<style lang="scss" scoped></style>

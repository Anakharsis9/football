<template>
  <div class="wrapper">
    <teams-table @teamsListUpdate="$emit('teamsListUpdate', $event)"></teams-table>
  </div>
</template>

<script>
import TeamsTable from "@/components/TeamsTable.vue";

export default {
  name: "InfoTables",
  components: {
    TeamsTable,
  },
  data: () => ({}),
};
</script>

<style lang="scss" scoped>

</style>

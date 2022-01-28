<template>
  <div class="wrapper">
    <teams-table></teams-table>
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
.wrapper {
  // display: flex;
  // justify-content: center;
}
</style>

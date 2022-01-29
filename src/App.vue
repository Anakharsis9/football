<template>
  <div id="app">
    <Field class="field" :teamsList="teamsList"></Field>
    <info-tables
      @teamsListUpdate="teamsList = $event"
      class="infoTables"
    ></info-tables>
  </div>
</template>

<script>
import Field from "@/components/Field.vue";
import InfoTables from "@/components/InfoTables.vue";

export default {
  name: "App",
  components: {
    Field,
    InfoTables,
  },
  data: () => ({
    teamsList: [],
  }),
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  outline: none;
  font-family: "Courier New", Courier, monospace;
}
#app {
  padding: 20px;
  overflow-x: hidden;
  display: grid;
  gap: 10px;
  grid-template-columns: 2fr 1fr;
  height: 100vh;
}

.addBtn {
  width: 180px;
  height: 40px;
  border: none;
  font-size: 18px;
  color: white;
  background-color: rgb(52, 67, 202);
  margin-top: 5px;
}
</style>

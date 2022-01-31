<template>
  <div class="field_wrapper">
    <match-settings
      :teamsList="teamsList"
      @settingModeChange="isSettingMode = $event"
      @twoTeams="twoTeams = $event"
    ></match-settings>
    <div class="field_container">
      <cells :team="twoTeams[0]" v-if="isSettingMode" class="team team1">
      </cells>
      <cells :team="twoTeams[1]" v-if="isSettingMode" class="team team2"> </cells>
    </div>
  </div>
</template>

<script>
import MatchSettings from "@/components/MatchSettings.vue";
import Cells from "@/components/Cells.vue";

export default {
  name: "Field",
  props: {
    teamsList: {
      type: Array,
    },
  },
  components: {
    MatchSettings,
    Cells,
  },
  data: () => ({
    isSettingMode: false,
    twoTeams: [],
  }),
  methods: {},
};
</script>

<style lang="scss" scoped>
.field_wrapper {
  display: flex;
  flex-direction: column;
}

.field_container {
  background-image: url("../assets/Field.svg");
  background-size: contain;
  background-repeat: no-repeat;
  width: 1000px;
  height: 750px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-content: center;
  align-items: center;
}

.team {
  margin-top: -50px;
  display: grid;
  width: 80%;
  height: 65%;
  grid-template: repeat(5, 1fr) / repeat(4, 1fr);
  justify-items: center;
  align-items: center;
}
.team1 {
  margin-left: 95px;
}
</style>

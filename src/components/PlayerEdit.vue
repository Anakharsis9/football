<template>
  <div class="wrapper">
    <button v-if="!isPlayerEdit" @click.stop="turnOnEdit">Edit</button>
    <button v-else @click.stop="editPlayer">Save</button>
    <div v-if="isPlayerEdit">
      <input v-model="player.fullName" type="text" />
      <input v-model="player.number" type="number" />
      <span style="color: red" v-if="playerError">
        Player with {{ playerNumber }} number exist. Please, choose another
        number.
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "PlayerEdit",
  props: {
    player: {
      type: Object,
      require: true,
    },
    numbers: {
      type: Object,
      require: true,
    },
  },
  data: () => ({
    isPlayerEdit: false,
    playerError: false,
  }),
  computed: {},
  methods: {
    turnOnEdit() {
      this.isPlayerEdit = true;
    },
    editPlayer() {
      if (this.numbers.includes(this.player.number)) return this.playerError = true;
      this.isPlayerEdit = false;
    },
  },
};
</script>

<style></style>

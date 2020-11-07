<template>
  <div class="text-center">
    <h1 class="mt-5">{{ message }}</h1>
    <b-row class="p-3 mb-5">
      <b-col class="shadow p-5 m-5">
        <b-spinner
          v-show="isPlayerTurn"
          type="grow"
          label="Loading..."
        ></b-spinner>

        <h1>Player</h1>
        <b-progress
          :value="playerHealth"
          :max="max"
          show-progress
          animated
          :variant="getPlayerStatus"
        ></b-progress>

        <div>
          <b-img
            src="https://media.giphy.com/media/frh24ti6yVTTW/giphy.gif"
            width="200px"
            fluid
          ></b-img>
        </div>

        <b-button
          variant="outline-danger"
          class="m-3"
          @click="playerAttack"
          :disabled="!isPlayerTurn"
          >Attack</b-button
        >
        <b-button
          variant="outline-success"
          class="m-3"
          @click="playerHeal"
          :disabled="!isPlayerTurn"
          >Heal</b-button
        >
      </b-col>
      <b-col class="shadow p-5 m-5">
        <b-spinner
          v-show="!isPlayerTurn"
          type="grow"
          label="Loading..."
        ></b-spinner>
        <h1>Monter</h1>

        <b-progress
          :value="monsterHealth"
          :max="max"
          show-progress
          animated
          :variant="getMonsterStatus"
        ></b-progress>

        <div>
          <b-img
            src="https://media.giphy.com/media/mCatcBTrqslfNU95sl/giphy.gif"
            width="300px"
            fluid
          ></b-img>
        </div>

        <b-button
          variant="outline-danger"
          class="m-3"
          @click="monsterAttack"
          :disabled="isPlayerTurn"
          >Attack</b-button
        >
        <b-button
          variant="outline-success"
          @click="monsterHeal"
          :disabled="isPlayerTurn"
          >Heal</b-button
        >
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "Content",
  data: () => ({
    message: "Welcome to Monster Attack Game !",
    num: 0,
    playerHealth: 100,
    monsterHealth: 100,
    playerStatus: "success",
    monsterStatus: "success",
    isPlayerTurn: true,
  }),
  computed: {
    getPlayerStatus() {
      if (this.playerHealth >= 70) {
        return "success";
      } else if (this.playerHealth > 30 && this.playerHealth < 70) {
        return "warning";
      } else {
        return "danger";
      }
    },
    getMonsterStatus() {
      if (this.monsterHealth >= 70) {
        return "success";
      } else if (this.monsterHealth > 30 && this.monsterHealth < 70) {
        return "warning";
      } else {
        return "danger";
      }
    },
  },
  watch: {
    playerHealth(value) {
      if (value < 0) {
        this.message = "Monster Win !";
      }
      if (value > 100) {
        this.playerHealth = 100;
        this.message = "Player ! You can't heal anymore !";
      }
    },
    monsterHealth(value) {
      if (value < 0) {
        this.message = "Player  Win !";
      }
      if (value > 100) {
        this.monsterHealth = 100;
        this.message = "Monster ! You can't heal anymore !";
      }
    },
  },
  methods: {
    playerAttack() {
      this.num = Math.floor(Math.random() * 20);
      this.monsterHealth -= this.num;
      this.message = "Player Attack Monster by " + this.num;
      this.isPlayerTurn = !this.isPlayerTurn;
    },
    playerHeal() {
      this.num = Math.floor(Math.random() * 20);
      this.playerHealth += this.num;
      this.message = "Player Heal by " + this.num;
      this.isPlayerTurn = !this.isPlayerTurn;
    },
    monsterAttack() {
      this.num = Math.floor(Math.random() * 20);
      this.playerHealth -= this.num;
      this.message = "Monster Attack Player by " + this.num;
      this.isPlayerTurn = !this.isPlayerTurn;
    },
    monsterHeal() {
      this.num = Math.floor(Math.random() * 20);
      this.monsterHealth += this.num;
      this.message = "Monster Heal by " + this.num;
      this.isPlayerTurn = !this.isPlayerTurn;
    },
  },
};
</script>

<style lang="scss" scoped></style>

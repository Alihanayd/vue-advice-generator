<template>
  <div class="home">
    <div class="main-container">
      <p class="text title">ADVICE #{{ slip.id }}</p>
      <div class="text advice">"{{ slip.advice }}"</div>

      <div class="divider">
        <div class="desktop-divider">
          <img src="../assets/pattern-divider-desktop.svg" alt="" />
        </div>
        <div class="mobile-divider">
          <img src="../assets/pattern-divider-mobile.svg" alt="" />
        </div>
      </div>
      <div class="button-container">
        <button @click="randomAdvice()" class="update-button">
          <img src="../assets/icon-dice.svg" alt="" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HomeView",
  data() {
    return {
      slip: {},
    };
  },
  mounted() {
    this.randomAdvice();
  },
  methods: {
    randomAdvice() {
      axios
        .get("https://api.adviceslip.com/advice")
        .then((response) => (this.slip = response.data.slip));
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: hsl(218, 23%, 16%);
}
.main-container {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  width: 600px;
  padding: 40px;
  border-radius: 20px;
  background-color: hsl(217, 19%, 24%);
  height: 400px;
}
.text {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: "Manrope", sans-serif;
  font-weight: 800;
}
.title {
  color: hsl(150, 100%, 66%);
  font-size: 14px;
  letter-spacing: 4px;
  margin-bottom: 20px;
}
.advice {
  font-size: 28px;
  color: hsl(193, 38%, 86%);
  text-align: center;
  margin-bottom: 80px;
  height: 120px;
}
.divider {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 40px;
}
.button-container {
  position: relative;
}
.update-button {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: hsl(150, 100%, 66%);
  border: none;
  border-radius: 50%;
  padding: 20px;
  cursor: pointer;
  position: absolute;
  top: 10px;
  left: calc(50% - 32px);
}
.update-button:hover {
  box-shadow: 0px 0px 20px 4px hsl(150, 100%, 66%);
}
.mobile-divider {
  display: none;
}
@media (max-width: 600px) {
  .main-container {
    width: 90%;
  }
  .advice {
    font-size: 20px;
  }
  .desktop-divider {
    display: none;
  }
  .mobile-divider {
    display: block;
  }
}
</style>

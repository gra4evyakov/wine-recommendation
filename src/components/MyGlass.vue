<template>
  <div class="state-ball mb-2 mx-auto align-self-end">
    <div class="wave" :class="{ white: color === 'white' }"></div>
  </div>
</template>

<script>
export default {
  props: ["color"],
};
</script>

<style scoped>
.state-ball {
  overflow: hidden;
  position: relative;
  padding: 2px;
  border: 2px solid rgba(0, 0, 0, 0.289);
  border-top: none;
  border-radius: 100%;
  width: 200px;
  height: 200px;
  background-color: inherit;
  z-index: 1;
}

.state-ball::before,
.state-ball::after {
  position: absolute;
  left: 40%;
  top: 0;
  z-index: 20;
  margin-left: -100px;
  width: 250px;
  height: 250px;
  content: "";
}

.state-ball::before {
  margin-top: -133px;
  border-radius: 45%;
  background-color: rgba(255, 255, 255, 0.5);
  animation: rotate 10s linear -5s infinite;
}

.state-ball::after {
  margin-top: -160px;
  border-radius: 40%;
  background-color: rgba(255, 255, 255, 0.8);
  animation: rotate 15s infinite;
}

.wave {
  position: relative;
  border-radius: 100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(-180deg, #ab0000 13%, rgb(86, 3, 3) 91%);
}

.wave.white {
  background: linear-gradient(-180deg, #aeb195 13%, #eff1c6 91%);
}

@keyframes rotate {
  to {
    transform: rotate(1turn);
  }
}
</style>

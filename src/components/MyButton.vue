<template>
  <button>
    <div class="wave"></div>
    <span>{{ label }}</span>
  </button>
</template>

<script>
export default {
  props: ["label"],
};
</script>

<style scoped>
button {
  font-size: 24px;
  letter-spacing: 2px;
  text-transform: uppercase;
  padding: 30px 30px 10px 30px;
  width: 100%;
  font-weight: 600;
  color: white;
  background-color: transparent;
  border: none;
  border-radius: 3px;
  position: relative;
  overflow: hidden;
  cursor: pointer;
}

button:hover .wave {
  top: -150px;
}

button span {
  position: relative;
}

button .wave {
  position: absolute;
  top: -100px;
  left: 0;
  width: 250px;
  height: 250px;
  background: linear-gradient(45deg, #65030c, #db0014);
  transition: 0.5s ease;
}

button .wave:after,
button .wave:before {
  content: "";
  position: absolute;
  width: 200%;
  height: 200%;
  top: 0;
  left: 50%;
  transform: translate(-50%, -75%);
}

button .wave:after {
  border-radius: 40%;
  background: rgba(255, 255, 255, 0.5);
  animation: wave 7s linear infinite;
}

button .wave:before {
  border-radius: 45%;
  background: #fbfbfb;
  animation: wave 12s linear infinite;
}

@keyframes wave {
  0% {
    transform: translate(-50%, -75%) rotate(0deg);
  }

  0% {
    transform: translate(-50%, -75%) rotate(360deg);
  }
}
</style>

<template>
  <div class="loader">
    <div class="loader-right"></div>
    <div class="loader-left"></div>
  </div>
</template>

<script>
export default {
  name: 'Timer',
  props: {
    timesUp: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      timeLeft: 15
    }
  },
  methods: {
    countDown () {

    }
  }
}
</script>

<style>
.loader {
  border-radius: 50%;
  width: 50px;
  height: 50px;
  background: #531e77;
  position: relative;
}

.loader::after {
  content: '';
  position: absolute;
  background: white;
  border-radius: 50%;
  height: 40px;
  width: 40px;
  top: 5px;
  left: 5px;
}

.loader .loader-right,
.loader .loader-left {
  width: 25px;
  height: 50px;
  position: absolute;
  z-index: 2;
  overflow: hidden;
}

.loader .loader-right::after,
.loader .loader-left::after,
.loader .loader-right::before,
.loader .loader-left::before {
  content: '';
  position: absolute;
  background: white;
  height: 40px;
  width: 40px;
  animation-duration: 15s;
  animation-timing-function: linear;
  animation-name: loading;
  animation-fill-mode: both;
}

.loader .loader-right {
  right: 0;
}

.loader .loader-right::after {
  right: -12.5px;
  top: -12.5px;
  transform-origin: 0 100%;
}

.loader .loader-right::before {
  right: -12.5px;
  bottom: -12.5px;
  transform-origin: 0 0;
}

.loader .loader-left {
  left: 0;
}

.loader .loader-left::after {
  opacity: 1;
  top: -12.5px;
  left: -12.5px;
  transform-origin: 100% 100%;
  animation-delay: 7s;
}

.loader .loader-left::before {
  opacity: 1;
  bottom: -12.5px;
  left: -12.5px;
  transform-origin: 100% 0;
  animation-delay: 7s;
}

@keyframes loading {
  0% {
    opacity: 1;
    transform: rotate(0deg);
  }

  50% {
    opacity: 1;
  }

  51% {
    opacity: 0;
  }

  100% {
    transform: rotate(360deg);
    opacity: 0;
  }
}
</style>

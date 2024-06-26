<template>
    <div class="stopwatch">
        <div class="circle">
            <div class="time-display mb-3">
            <h1 :class="{ 'blink-orange': isBlinking }">{{ formattedTime }}</h1>
            </div>
        </div>
      
      <div class="buttons">
        <b-button @click="startPause" variant="primary" class="mr-2">
            <b-icon v-if="!isRunning" icon="play-fill" font-scale="1.3"></b-icon>
            <b-icon v-else icon="pause-fill"></b-icon>
      </b-button>
      <b-button @click="stop" variant="danger" class="mr-2">Stop <b-icon font-scale="1.3" icon="stop-fill"></b-icon></b-button>
      <b-button @click="reset" variant="secondary" :disabled="isRunning"><b-icon icon="arrow-repeat"></b-icon></b-button>
      </div>
    </div>
  </template>
  
  <script>
export default {
  name: 'StopWatch',
  data() {
    return {
      time: 0,
      isRunning: false,
      interval: null,
      showingFinalTime: false,
      isBlinking: false,
    }
  },
  computed: {
    formattedTime() {
      const minutes = Math.floor(this.time / 60000)
      const seconds = Math.floor((this.time % 60000) / 1000)
      const centiseconds = Math.floor((this.time % 1000) / 10)

      return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}:${centiseconds.toString().padStart(2, '0')}`
    }
  },
  methods: {
    startPause() {
      if (this.isRunning) {
        this.pause()
      } else {
        this.start()
      }
    },
    start() {
      this.isRunning = true
      const startTime = Date.now() - this.time
      this.interval = setInterval(() => {
        this.time = Date.now() - startTime
      }, 10) // Update every 10 millisecond
    },
    pause() {
      this.isRunning = false
      clearInterval(this.interval)
    },
    stop() {
      this.pause()
      this.showingFinalTime = true

      this.isBlinking = true
      
      // Start blinking
      const blinkInterval = setInterval(() => {
        this.isBlinking = !this.isBlinking
      },300) 
      
      setTimeout(() => {
        clearInterval(blinkInterval)
        this.isBlinking = false
        this.time = 0
        this.showingFinalTime = false
      }, 6000)
    },
    reset() {
      if (!this.isRunning && !this.showingFinalTime) {
        this.time = 0
      }
    }
  }
}
</script>
  
  <style scoped>
  .mr-2 {
    margin-right: 1rem;
  }
  .mb-3 {
    margin-bottom: 1rem;
  }
  .circle {
    margin-bottom: 50px;
    padding-top: 10%;
    border-radius: 100%;
    border: 0.5em solid #73AD21;
    height: 300px;
    width: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #010127;;
  }
  .blink-orange {
  color:#8cc4fd;
}
@keyframes blink {
  0% { opacity: 1; }
  50% { opacity: 0; }
  100% { opacity: 1; }
}
.blink-orange {
  animation: blink 1s linear infinite;
}

  </style>
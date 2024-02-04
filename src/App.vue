<script>
export default {
  data() {
    return {
      perspective: 100,
      rotateX: 0,
      rotateY: 0,
      rotateZ: 0,
      alertText: '',
      successAlert: false,
      infoAlert: false,
    }
  },
  computed: {
    box() {
      return {
        transform: `  perspective(${this.perspective}px)
                      rotateX(${this.rotateX}deg)
                      rotateY(${this.rotateY}deg)
                      rotateZ(${this.rotateZ}deg) `,
      }
    },

    alertStyle() {
      return {
        'info-alert': this.infoAlert,
        'success-alert': this.successAlert,
      }
    },
  },
  methods: {
    reset() {
      this.perspective = 100
      this.rotateX = 0
      this.rotateY = 0
      this.rotateZ = 0
      this.alertText = 'Style Got Reset'
      this.infoAlert = true
      if (this.successAlert) this.successAlert = false
    },
    copy() {
      let text = `transform:   perspective(${this.perspective}px)
                      rotateX(${this.rotateX}deg)
                      rotateY(${this.rotateY}deg)
                      rotateZ(${this.rotateZ}deg) `
      navigator.clipboard.writeText(text)
      this.alertText = 'Style Got Copied'
      this.successAlert = true
      if (this.infoAlert) this.infoAlert = false
    },
    close() {
      this.alertText = ''
      if (this.infoAlert) this.infoAlert = false
      if (this.successAlert) this.successAlert = false
    },
  },
}
</script>

<template>
  <main>
    <div v-show="alertText" class="alert" :class="alertStyle">
      <p>
        <span class="alert-text">{{ alertText }} 👍</span>
        <span class="alert-close" @click.prevent="close">&times;</span>
      </p>
    </div>
    <div class="container">
      <h1>CSS3 Perspective Playground</h1>
      <div class="wrapper">
        <div class="left-side">
          <label
            ><span>perspective: {{ perspective }}px;</span
            ><input type="range" max="999" min="0" v-model="perspective"
          /></label>
          <label
            ><span>rotateX: {{ rotateX }}deg;</span
            ><input type="range" max="180" min="-180" v-model="rotateX"
          /></label>
          <label
            ><span>rotateY: {{ rotateY }}deg;</span
            ><input type="range" max="180" min="-180" v-model="rotateY"
          /></label>
          <label
            ><span>rotateZ: {{ rotateZ }}deg;</span
            ><input type="range" max="180" min="-180" v-model="rotateZ"
          /></label>
          <div class="btn-group">
            <button class="reset" @click.prevent="reset">RESET</button>
            <button class="copy" @click.prevent="copy">COPY</button>
          </div>
        </div>
        <div class="right-side">
          <div class="outer-box">
            <div class="inner-box" :style="box"></div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  width: 100vw;
  height: 90rem;
  font-family: 'Poppins', sans-serif;
}

.container {
  width: 50rem;
  height: 50rem;
  margin: 70px auto;
  padding: 30px;
}

.container h1 {
  text-align: center;
  font-style: oblique;
  white-space: nowrap;
  letter-spacing: 0.2rem;
}

.outer-box {
  width: 20rem;
  height: 20rem;
  border: 2px solid gray;
  border-radius: 0.4rem;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.3);
}

.inner-box {
  width: 10rem;
  height: 10rem;
  background-color: orangered;
  border-radius: 0.4rem;
}

.wrapper {
  display: flex;
  align-items: center;
}

.left-side,
.right-side {
  padding: 5rem;
}

label {
  font-style: oblique;
  letter-spacing: 0.2rem;
  color: #fff;
}

button {
  padding: 0.6rem 1.2rem;
  font-size: 1.4rem;
  margin-right: 3rem;
  border: none;
  border-radius: 0.4rem;
  color: #fff;
  cursor: pointer;
  font-weight: bold;
}

.btn-group {
  display: flex;
  margin-top: 2rem;
}

.left-side {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.copy {
  background-color: #2a9d8f;
}

.reset {
  background-color: #7209b7;
}

.container h1 {
  color: #8338ec;
  font-weight: bold;
}

input {
  width: 16rem;
  cursor: pointer;
}

.close {
  background-color: rgb(144, 4, 4);
}

.alert {
  padding: 20px;
  background-color: #04aa6d;
  color: #fff;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.3);
}

.alert p {
  text-align: center;
}
.alert-close {
  float: right;
  font-size: 22px;
  cursor: pointer;
  vertical-align: middle;
  font-weight: bold;
}

.alert-text {
  vertical-align: middle;
  font-weight: bold;
  letter-spacing: 1px;
  font-style: oblique;
  font-size: 18px;
}

.info-alert {
  background-color: #2196f3;
}

.success-alert {
  background-color: #04aa6d;
}
</style>

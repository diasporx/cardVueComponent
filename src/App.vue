<template>
  <Main />
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.w-100 {
  width: 100%;
}
.d-flex {
  display: flex;
}
.flex-column {
  flex-direction: column;
}
.align-items-center {
  align-items: center;
}
.justify-content-center {
  justify-content: center;
}
.justify-content-between {
  justify-content: space-between;
}
.mb-1 {
  margin-bottom: 15px;
}
.me-1 {
  margin-right: 10px;
}
.mb-2 {
  margin-bottom: 20px;
}
body {
  min-height: 100vh;
  font-size: 18px;
}

@font-face {
  font-family: 'Space';
  src: url('./assets/font/SpaceGrotesk-Regular.ttf');
  font-weight: 400;
}

@font-face {
  font-family: 'Space';
  src: url('./assets/font/SpaceGrotesk-Medium.ttf');
  font-weight: 500;
}

@font-face {
  font-family: 'Space';
  src: url('./assets/font/SpaceGrotesk-Light.ttf');
  font-weight: 300;
}

@font-face {
  font-family: 'Space';
  src: url('./assets/font/SpaceGrotesk-Bold.ttf');
  font-weight: 700;
}

#app {
  font-family: 'Space';
  font-weight: 500;
}</style>

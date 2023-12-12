`~`<template>
  <div class="area-wrapper">
    <div class="area">
      <router-view />
    </div>
  </div>
</template>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: sans-serif;
}

ul {
  list-style: none;
}

.area {
  color: rgb(0, 0, 0);
  width: 1500px;
  margin: 0 auto;
  overflow: hidden;
}

.area-wrapper {
  width: 100%;
  height: 100vh;

  background-color: #979797;
}
</style>

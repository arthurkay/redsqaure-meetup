<template>
  <div id="app">
    <div id="nav">
      <div class="top-bar shadow-lg p-3 mb-5 bg-white rounded">
        <span class="app-name">
          <span class="text-white bg-danger">  Living Open Source </span>|meetapp
        </span>
        <span class="float-right">
          <router-link to="/">Home</router-link> |
          <router-link to="/about">About</router-link>
        </span>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<style>
.top-bar {
  height: 80px;
  margin: auto;
}
.app-name {
  font-size: 25px;
}
a:hover {
  color: red;
}
#nprogress .bar {
background: #f00 !important;
}
</style>

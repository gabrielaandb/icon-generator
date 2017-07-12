<template>
  <div id="app">
    <div id="box" v-bind:style="{ width: fontSize, height: fontSize, backgroundColor: background}">
      <i class="material-icons" v-bind:style="{ color: color, fontSize: fontSize}">{{ icon }}</i>
    </div>
    <br><br>
    <input v-model="icon" placeholder="icon"><br>
    <input v-model="fontSize" placeholder="size"><br>
    <input v-model="color" placeholder="color"><br>
    <input v-model="background" placeholder="background"><br>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      icon: 'fingerprint',
      fontSize: '300px',
      color: '#123456',
      background: 'white',
    }
  },
  methods: {
    loadParams () {
      var size = getParameterByName(size);
      alert(size);
    },
    getParameterByName (name, url) {
      if (!url) url = window.location.href;
      name = name.replace(/[\[\]]/g, "\\$&");
      var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
          results = regex.exec(url);
      if (!results) return null;
      if (!results[2]) return '';
      return decodeURIComponent(results[2].replace(/\+/g, " "));
  }
  },
  beforeMount () {
    var icon = this.getParameterByName('icon');
    var size = this.getParameterByName('size');
    var color = this.getParameterByName('color');

    if (size) this.fontSize = size;
    if (color) this.color = color;
    if (icon) this.icon = icon;

    if (color[0] == '*') {
      this.color = '#' + color.substring(1);
    }
  }
}
</script>

<style>
body {
  background-color: black;
}
#app {
  padding:25px;
  background-color: black;
}
#box {
  margin-right: auto;
  margin-left: auto;
  background-color: white;
}
</style>

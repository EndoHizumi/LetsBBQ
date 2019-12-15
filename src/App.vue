<template>
  <div id="app">
    <div id="header">
      <h1>Welcome to Lets-BBQ App</h1>
      <p>{{message}}</p>
      <p>
        <span>controller:</span>
        <button id="add" v-on:click="addSushi">Add</button>
        <button id="reduce" v-on:click="reduceSushi">Reduce</button>
      </p>
    </div>
    <ul @wheel="onScroll" v-bind:class="state">
      <li v-for="number in numbers" v-bind:key="number">
        <Meat v-bind:state="state" />
      </li>
    </ul>
  </div>
</template>

<script>
import Meat from "./components/meat";
export default {
  name: "app",
  timeoutId: 0,
  data() {
    return {
      state: "stop",
      message:
        "Burn the meat with the scroll! The grilled meat is delicious!",
      numbers: [0]
    };
  },
  mounted() {
    document.addEventListener("wheel", this.onScroll);
  },
  components: {
    Meat
  },
  methods: {
    toggle() {
      if (this.state == "spin") {
        this.state = "stop";
        this.message = "oh? were you full of stomach?";
      } else {
        this.state = "spin";
        this.message =
          "Japanese Common People Supporter is kaiten-zushi. I expressed gratitude for that kaiten-zushi.";
      }
    },
    addSushi() {
      this.numbers.push(0);
    },
    reduceSushi() {
      if (this.numbers.length > 1) {
        this.numbers.pop();
      }
    },
    onScroll() {
      /* eslint-disable no-console */
      this.state = "spin";
      clearTimeout(this.timeoutId);
      const vue = this
      this.timeoutId = setTimeout(function() {
        vue.state = "stop"
      }, 350);
    }
  }
};
</script>

<style>
ul {
  background-color: black;
  background-image: url("./assets/mesh.png");
  background-repeat: no-repeat;
  background-position: top center, left, center;
  background-size: cover;
}

ul.spin{
  background-image:url("./assets/mesh.png"), url("./assets/burn.gif");
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul li {
  display: inline;
}
</style>

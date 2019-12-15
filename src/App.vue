<template>
  <div id="app">
    <div id="header">
      <h1>Welcome to Lets-BBQ App</h1>
      <p>{{message}}</p>
      <span>mode:</span>
      <button v-on:click="toggle">{{mode}}</button>
      <p>
        <span>controller:</span>
        <button id="add" v-on:click="addSushi">Add</button>
        <button id="reduce" v-on:click="reduceSushi">Reduce</button>
      </p>
    </div>
    <ul v-bind:wheel="onScroll" v-on:click="onClick" v-bind:class="state">
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
      mode: "while",
      message: "Burn the meat with the scroll! The grilled meat is delicious!",
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
      if (this.mode == "while") {
        this.mode = "toggle";
        this.message = "Burn the meat with the click on mesh!! The grilled meat is delicious!"
      } else {
        this.mode = "while";
        this.message = "Burn the meat with the scroll!! The grilled meat is delicious!"
      }
    },
    onScroll() {
      if (this.mode == "while") {
        this.whileSpin()
      }
    },
    onClick(){
      if (this.mode == "toggle") {
        this.toggleSpin()
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
      /* eslint-disable no-console */
    whileSpin() {
      this.state = "spin";
      console.log(this.state)
      clearTimeout(this.timeoutId);
      const vue = this;
      this.timeoutId = setTimeout(function() {
        vue.state = "stop";
      }, 350);
    },
    toggleSpin() {
      console.log(this.state)
      if (this.state == "spin") {
        this.state = "stop";
      } else {
        this.state = "spin";
      }
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

ul.spin {
  background-image: url("./assets/mesh.png"), url("./assets/burn.gif");
}

Meat {
  filter: brightness(-127%);
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

<template>
  <div v-bind:class="state" id="meat"><span id="chara_meat">🥩</span></div>
</template>

<script>
export default {
  name: "meat",
  props: {
    state: String
  }
};
</script>

<style>

#meat {
  font-family: "Segoe UI Emoji", "Segoe UI Symbol", "Apple Color Emoji",
    "Noto Color Emoji", "Noto Emoji", sans-serif;
  font-size: 1500%;
  margin-left: auto;
  margin-right: auto;
  display: inline-block;
}

#meat.spin {
  animation: spin 1.5s linear infinite;
}

#meat.burnt {
  filter: grayscale(100%);
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>


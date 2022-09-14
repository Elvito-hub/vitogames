<template>
  <Header />
  <QuizPart v-if="countriesData.length > 0" :countries="countriesData" />
</template>

<script>
import Header from "./components/Header.vue";
import QuizPart from "./components/QuizPart.vue";
export default {
  name: "App",
  components: {
    Header,
    QuizPart,
  },
  data() {
    return {
      countriesData: [],
    };
  },
  mounted() {
    fetch("https://restcountries.com/v3.1/all")
      .then((response) => response.json())
      .then((res) => {
        // console.log(res);
        this.countriesData = res;
        console.log(this.countriesData[0]);
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

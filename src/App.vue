<template>
  <v-app>
    <v-main>
      <Header />
      <QuizPart v-if="countriesData.length > 0" :countries="countriesData" />
    </v-main>
  </v-app>
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
    fetch("https://restcountries.com/v3.1/region/africa")
      .then((response) => response.json())
      .then((res) => {
        // console.log(res);
        this.countriesData = res;
        console.log(this.countriesData[0]);
      });
  },
};
</script>

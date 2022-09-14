<template>
  <div>
    <v-card class="d-flex flex-row mb-6" :color="$vuetify.theme.dark ? 'grey darken-3' : 'grey lighten-4'" flat tile>
      <v-card :key="item" v-for="item in countryCp" class="pa-2" outlined tile>
        {{ item }}
      </v-card>
    </v-card>
  </div>
</template>

<script>
import vuetify from "vuetify";
export default {
  name: "QuizPart",
  data() {
    return {
      countryCp: [],
    };
  },
  props: {
    countries: Array,
  },
  methods: {
    shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        const temp = array[i];
        array[i] = array[j];
        array[j] = temp;
      }
      return array;
    },
  },
  mounted() {
    console.log(this.countries);
    var countcapientries = [];
    var countriescapitals = this.countries.map((item) => {
      if (item.capital != undefined) {
        var countcap = {};
        var countname = item.name.common;
        countcap[`${countname}`] = item.capital[0];
        countcapientries.push(item.name.common);
        countcapientries.push(item.capital[0]);
        return countcap;
      }
    });
    const shuffledarray = this.shuffleArray(countcapientries);
    this.countryCp = shuffledarray;
  },
};
</script>

<style>
.gamebutton {
  display: flex;
  flex-direction: column;
}
</style>

<template>
  <div>
    <v-card class="d-flex flex-wrap" :color="$vuetify.theme.dark ? 'grey darken-3' : 'grey lighten-4'" flat tile>
      <v-btn @click="toggleselect(item)" :color="selectedPairs.includes(item) ? 'red' : ''" v-for="item in countryCp" class="pa-2 ma-2" outlined tile>
        {{ item }}
      </v-btn>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "QuizPart",
  data() {
    return {
      countryCp: [],
      selectedPairs: [],
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
    toggleselect(item) {
      console.log(this.selectedPairs);
      if (this.selectedPairs.length == 0) {
        this.selectedPairs = [...this.selectedPairs, item];
      } else {
        this.selectedPairs = [...this.selectedPairs, item];
        var found = false;
        this.countries.map((item) => {
          if (item.capital != undefined && this.selectedPairs.includes(item.capital[0]) && this.selectedPairs.includes(item.name.common)) {
            found = true;
          }
        });
        if (found) {
          this.countryCp = this.countryCp.filter((item) => {
            if (!this.selectedPairs.includes(item)) {
              return item;
            }
          });
        }
        this.selectedPairs = [];
      }
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
    console.log(shuffledarray);
  },
};
</script>

<style>
.gamebutton {
  display: flex;
  flex-direction: column;
}
</style>

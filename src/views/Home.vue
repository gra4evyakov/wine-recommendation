<template>
  <v-app>
    <v-main class="card d-flex flex-column">
      <v-btn
        to="/auth"
        @click="logOut"
        height="50px"
        width="50px"
        class="btn_logout"
        :color="wineColor === 'white' ? 'lime-lighten-4' : 'red'"
        icon="mdi-logout"
      ></v-btn>
      <v-tabs
        v-model="wineColor"
        :bg-color="wineColor === 'white' ? 'lime-lighten-4' : 'red'"
        align-tabs="center"
        fixed-tabs
      >
        <v-tab value="red">Red wine</v-tab>
        <v-tab value="white">White wine</v-tab>
      </v-tabs>
      <v-tabs
        v-model="wineService"
        :bg-color="wineColor === 'white' ? 'lime-lighten-4' : 'red'"
        direction="vertical"
      >
        <v-tab value="dish">Dish for Wine</v-tab>
        <v-tab value="recommendation">Wine Recommendation</v-tab>
      </v-tabs>

      <!--DISH-->
      <v-card-text v-if="!loading && wineService === 'dish'">
        <div class="d-flex flex-column">
          <div class="d-flex flex-column justify-center">
            <my-selector
              @setWine="setWine"
              :color="wineColor"
              :wineList="currentWineData"
            />
            <v-btn
              @click="fetchWine(currentWine)"
              :color="wineColor === 'white' ? 'lime-lighten-4' : 'red'"
              append-icon="mdi-glass-wine"
            >
              Wine, please
            </v-btn>
          </div>
        </div>
        <v-card-text
          v-if="dishForWine"
          class="text-h4 text-center text-uppercase"
          >{{ dishForWine.title }}</v-card-text
        >
        <v-card-text v-if="dishForWine" class="text-h6 text-center">{{
          dishForWine.text
        }}</v-card-text>
      </v-card-text>
      <!--DISH-->

      <!--RECOMENDATION-->
      <v-card-text v-if="!loading && wineService === 'recommendation'">
        <div class="d-flex flex-column">
          <my-selector
            @setWine="setWine"
            :color="wineColor"
            :wineList="currentWineData"
          />
          <my-range @setRecomendation="setRecomendation" :color="wineColor" />
          <v-btn
            @click="fetchRecomendation()"
            :color="wineColor === 'white' ? 'lime-lighten-4' : 'red'"
            append-icon="mdi-glass-wine"
          >
            Wine, please
          </v-btn>
        </div>

        <div v-if="recomendationForWine">
          <my-card :recomendationForWine="recomendationForWine" />
        </div>
      </v-card-text>
      <!--RECOMENDATION-->

      <!--LOADER-->
      <div v-if="loading" class="d-flex flex-column align-center pt-10">
        <v-avatar class="mb-4" size="100"></v-avatar>
        <v-progress-circular
          indeterminate
          :color="wineColor === 'white' ? 'lime-darken-1' : 'red'"
        ></v-progress-circular>
      </div>
      <!--LOADER-->
      <my-glass v-if="!loading" :color="wineColor" />
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
import MyGlass from "../components/MyGlass.vue";
import MySelector from "@/components/MySelector.vue";
import MyRange from "@/components/MyRange.vue";
import MyCard from "@/components/MyCard.vue";
export default {
  components: {
    MyGlass,
    MySelector,
    MyRange,
    MyCard,
  },
  methods: {
    logOut() {
      localStorage.removeItem("accessToken");
    },
    setWine(value) {
      this.currentWine = value;
    },
    setRecomendation(recomendation) {
      this.currentRecomendation.maxPrice = recomendation.maxPrice;
      this.currentRecomendation.number = recomendation.number;
    },
    fetchWine(value) {
      this.loading = true;
      axios
        .get(
          `https://api.spoonacular.com/food/wine/dishes?apiKey=3612b3a030574b09aeeebb9aeeec44e2&wine=${value}`
        )
        .then((res) => {
          setTimeout(() => (this.loading = false), 3000);
          if (res.data.message) this.dishForWine.text = res.data.message;
          if (res.data.text) this.dishForWine.text = res.data.text;
          this.dishForWine.title = value;
        })
        .catch((error) => {
          setTimeout(() => (this.loading = false), 3000);
          console.log(error);
        });
    },
    fetchRecomendation(value) {
      this.loading = true;
      axios
        .get(
          `https://api.spoonacular.com/food/wine/recommendation?apiKey=3612b3a030574b09aeeebb9aeeec44e2&wine=${this.currentWine}&maxPrice=${this.currentRecomendation.maxPrice}&number=${this.currentRecomendation.number}`
        )
        .then((res) => {
          setTimeout(() => (this.loading = false), 3000);
          this.recomendationForWine = res.data.recommendedWines;
        })
        .catch((error) => {
          setTimeout(() => (this.loading = false), 3000);
          console.log(error);
        });
    },
  },
  data: () => ({
    currentWine: null,
    currentRecomendation: {},
    loading: false,
    dishForWine: {},
    recomendationForWine: {},
    wineColor: "red",
    wineService: "dish",
    white_wine: {
      dry_white_wine: [
        "assyrtiko",
        "pinot_blanc",
        "cortese",
        "roussanne",
        "moschofilero",
        "muscadet",
        "viognier",
        "verdicchio",
        "greco",
        "marsanne",
        "white_burgundy",
        "chardonnay",
        "gruener_veltliner",
        "white_rioja",
        "frascati",
        "gavi",
        "l_acadie_blanc",
        "trebbiano",
        "sauvignon_blanc",
        "catarratto",
        "albarino",
        "arneis",
        "verdejo",
        "vermentino",
        "soave",
        "pinot_grigio",
        "dry_riesling",
        "torrontes",
      ],
      mueller_thurgau: [],
      grechetto: [],
      gewurztraminer: [],
      chenin_blanc: [],
      white_bordeaux: [],
      semillon: [],
      riesling: [],
      sauternes: [],
      sylvaner: [],
      lillet_blanc: [],
    },
    red_wine: {
      dry_red_wine: [
        "petite_sirah",
        "zweigelt",
        "baco_noir",
        "bonarda",
        "cabernet_franc",
        "bairrada",
        "barbera_wine",
        "primitivo",
        "pinot_noir",
        "nebbiolo",
        "dolcetto",
        "tannat",
        "negroamaro",
        "red_burgundy",
        "corvina",
        "rioja",
        "cotes_du_rhone",
        "grenache",
        "malbec",
        "zinfandel",
        "sangiovese",
        "carignan",
        "carmenere",
        "cesanese",
        "cabernet_sauvignon",
        "aglianico",
        "tempranillo",
        "shiraz",
        "mourvedre",
        "merlot",
        "nero_d_avola",
      ],
      bordeaux: [],
      marsala: [],
      port: [],
      gamay: [],
      dornfelder: [],
      concord_wine: [],
      sparkling_red_wine: [],
      pinotage: [],
      agiorgitiko: [],
    },
  }),
  computed: {
    currentWineData() {
      return this.wineColor === "red" ? this.red_wine : this.white_wine;
    },
  },
};
</script>
<style scoped>
.v-application {
  min-width: 320px;
  max-width: 420px;
  margin: 0 auto;
  border-left: 1px solid black;
  border-right: 1px solid black;
}
.v-tabs--density-default {
  --v-tabs-height: 80px;
}

.card {
  border-radius: 0 !important;
}

.btn_logout {
  position: fixed;
  bottom: 10px;
  font-weight: bold;
  border: 1px solid rgb(85, 85, 85);
  z-index: 999;
}

.btn_logout.red {
  color: white;
  background: #65030c;
}

.btn_logout.white {
  color: black;
  background: #eff1c6;
}
</style>

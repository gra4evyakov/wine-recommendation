<template>
  <div>
    <v-autocomplete
      @blur="setWine"
      v-model="selectedtWine"
      :color="color === 'white' ? 'grey-darken-3' : 'red'"
      label="Select wine"
      :items="wineLists"
      variant="underlined"
    >
    </v-autocomplete>
    <v-autocomplete
      @blur="setWine"
      v-model="currentWine"
      v-if="subListIsVisible"
      :color="color === 'white' ? 'grey-darken-3' : 'red'"
      label="Select wine"
      :items="wineList[selectedtWine]"
      variant="underlined"
    >
    </v-autocomplete>
  </div>
</template>
s
<script>
export default {
  props: ["wineList", "color"],
  data() {
    return {
      selectedtWine: null,
      currentWine: null,
    };
  },
  emits: ["setWine"],
  methods: {
    setWine() {
      this.$emit("setWine", this.wineForFetch);
    },
  },
  computed: {
    wineLists() {
      return Object.keys(this.wineList);
    },
    subListIsVisible() {
      if (this.selectedtWine != null) {
        return this.wineList[this.selectedtWine].length > 0 ? true : false;
      } else {
        return false;
      }
    },
    wineForFetch() {
      return this.subListIsVisible ? this.currentWine : this.selectedtWine;
    },
  },
  watch: {
    wineLists() {
      this.selectedtWine = null;
      this.currentWine = null;
    },
  },
};
</script>

<style scoped></style>

<template>
  <div>
    <v-text-field
      @blur="setRecomendation"
      v-model="recomendation.maxPrice"
      :color="color === 'white' ? 'grey-darken-3' : 'red'"
      label="Max price $"
      variant="underlined"
    ></v-text-field>
    <v-text-field
      @blur="setRecomendation"
      v-model="recomendation.number"
      :color="color === 'white' ? 'grey-darken-3' : 'red'"
      label="Quantity"
      variant="underlined"
    ></v-text-field>
  </div>
</template>

<script>
export default {
  data() {
    return {
      recomendation: {
        maxPrice: null,
        number: null,
      },
    };
  },
  emits: ["setRecomendation"],
  props: ["color"],
  methods: {
    setRecomendation() {
      this.$emit("setRecomendation", this.recomendation);
    },
  },
};
</script>

<style scoped></style>

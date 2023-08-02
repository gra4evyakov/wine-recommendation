<template>
    <!-- <v-card v-for="wine in recomendationForWine" class="mx-auto" max-width="344">
        <v-img :src="wine.imageUrl" height="200px"></v-img>
        <v-card-title>
            {{ wine.title }}
        </v-card-title>
        <v-card-subtitle>
            {{ wine.price }}
        </v-card-subtitle>
        <v-card-actions>
            <v-btn color="orange-lighten-2" variant="text">
                About
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'" @click="show = !show"></v-btn>
        </v-card-actions>
        <v-expand-transition>
            <div v-show="show">
                <v-divider></v-divider>
                <v-card-text>
                    {{ wine.description }}
                </v-card-text>
            </div>
        </v-expand-transition>
    </v-card> -->
    <v-card
    v-for="wine in recomendationForWine"
    :loading="loading"
    class="mx-auto my-12"
    max-width="374"
  >
    <template v-slot:loader="{ isActive }">
      <v-progress-linear
        :active="isActive"
        color="deep-purple"
        height="4"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      :src="wine.imageUrl"
    ></v-img>

    <v-card-item>
      <v-card-title>{{ wine.title }}</v-card-title>
    </v-card-item>

    <v-card-text>
      <v-row
        align="center"
        class="mx-0"
      >
        <v-rating
          :model-value="wine.ratingCount"
          color="amber"
          density="compact"
          half-increments
          readonly
          size="small"
        ></v-rating>
      </v-row>

      <div class="my-4 text-subtitle-1">
        {{ wine.price }}
      </div>

      <div>{{ wine.description }}</div>
    </v-card-text>

    <v-divider class="mx-4 mb-1"></v-divider>

    <v-card-title>
        <a style="color: black; text-decoration: none;" :href="wine.link">Buy now</a>
    </v-card-title>
  </v-card>
</template>

<script>
export default {
    data() {
        return {
            loading: false,
            selection: 1,
        }
    },
    props:['recomendationForWine'],
    methods: {
      reserve () {
        this.loading = true
        setTimeout(() => (this.loading = false), 2000)
      },
    },
}
</script>

<style scoped>

</style>
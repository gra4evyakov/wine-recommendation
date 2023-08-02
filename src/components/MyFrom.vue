<template>
  <v-sheet class="h-screen d-flex flex-column justify-center pa-12">
    <v-card class="mx-auto px-6 py-8" max-width="344">
      <v-card-title class="text-h4 text-uppercase text-center">
        WineR
        <v-avatar
          class="mx-auto"
          image="@/assets/logo.png"
          size="80"
        ></v-avatar>
      </v-card-title>
      <v-form @submit.prevent="onSubmit">
        <v-text-field
          color="wine"
          v-model="login"
          :rules="[required]"
          class="mb-2"
          clearable
          label="Login"
        ></v-text-field>
        <v-text-field
          color="wine"
          v-model="password"
          :rules="[required]"
          clearable
          label="Password"
          placeholder="Enter your password"
        ></v-text-field>
        <div class="fill-height">
          <v-btn @click="setLoginAndPassword" block>
            Forgot log and pass
          </v-btn>
        </div>
        <br />
        <MyButton type="submit" label="Login" />
      </v-form>
    </v-card>
  </v-sheet>
</template>

<script>
import MyButton from "@/components/MyButton.vue";
export default {
  data: () => ({
    login: null,
    password: null,
  }),
  components: {
    MyButton,
  },
  methods: {
    setLoginAndPassword() {
      this.login = "admin";
      this.password = "admin";
    },
    onSubmit() {
      if (this.login === "admin" && this.password === "admin") {
        let token = Math.random().toString(36).slice(2);
        localStorage.setItem("accessToken", token);
        localStorage.setItem("currentUser", this.login.toString());
        let array = [];
        if (!localStorage.getItem(this.login.toString()))
          localStorage.setItem(this.login.toString(), JSON.stringify(array));
        this.$router.push("/");
      }
    },
    required(v) {
      return !!v || "Field is required";
    },
  },
};
</script>

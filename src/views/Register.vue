<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="mt-6 col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Sign Up</h1>
          <p class="text-xs-center">
            <router-link :to="{ name: 'login' }">Have an account?</router-link>
          </p>
          <mcv-validation-errors
            v-if="validationErrors"
            :validation-errors="validationErrors"
          />
          <form @submit.prevent="onSubmit">
            <fieldset class="form-group">
              <input
                type="text"
                class="form-control form-control-lg"
                placeholder="Username"
                v-model="username"
              />
            </fieldset>
            <fieldset class="form-group">
              <input
                type="text"
                class="form-control form-control-lg"
                placeholder="Email"
                v-model="email"
              />
            </fieldset>
            <fieldset class="form-group">
              <input
                type="password"
                class="form-control form-control-lg"
                placeholder="Password"
                v-model="password"
              />
            </fieldset>
            <v-btn
              text
              class="mr-4 primary"
              type="submit"
              :disabled="isSubmitting"
            >
              Sign Up
            </v-btn>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import McvValidationErrors from "@/components/ValidationErrors";
import { actionTypes } from "@/store/modules/auth";

export default {
  name: "McvRegister",
  components: {
    McvValidationErrors,
  },
  data: () => ({
    email: "",
    username: "",
    password: "",
  }),
  computed: {
    ...mapState({
      isSubmitting: (state) => state.auth.isSubmitting,
      validationErrors: (state) => state.auth.validationErrors,
    }),
  },
  methods: {
    onSubmit() {
      console.log("Submitted form...");
      this.$store
        .dispatch(actionTypes.register, {
          email: this.email,
          username: this.username,
          password: this.password,
        })
        .then((result) => {
          console.log("Succesfully register user", result);
          this.$router.push({ name: "Home" });
        });
    },
  },
};
</script>

<style></style>

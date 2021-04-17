<template>
  <v-app>
    <v-card color="white" flat height="9rem">
      <v-toolbar min-width="44rem" flat height="133">
        <v-toolbar-items min-width="1rem">
          <v-avatar width="12rem" min-width="2rem" color="#fff" size="100" tile flat>
            <v-img
              src="../../../../src/assets/logo_base.png"/></v-avatar
        ></v-toolbar-items>

        <v-spacer></v-spacer>

        <v-toolbar-title class="right-text pa-8">
          Don't have an account?
        </v-toolbar-title>

        <v-btn x-large color="#fff" class="right-btn">
          Sign up
        </v-btn>
      </v-toolbar>
    </v-card>
    <!-- resizing the content -->
    <v-main min-width="40rem">
      <v-container class="container">
        <v-card
          min-width="20rem"
          class="mx-auto mt-5 pa-5 text-center rounded-lg"
          id="limited-products"
        >
          <div class="text-center tilte ma-9">Let's go!</div>

          <v-container class="cardContainer">
            <v-form>
              <div class="text-left label">
                Email
              </div>
              <v-text-field
                v-model="email"
                type="text"
                placeholder="Enter your email"
                required
                persistent-hint
                outlined
                prepend-inner-icon="drafts"
                class="field"
              >
                {{ email }}</v-text-field
              >

              <div class="text-left label">
                Password
              </div>
              <v-text-field
                placeholder="Enter password"
                v-model="password"
                type="password"
                required
                persistent-hint
                outlined
                prepend-inner-icon="lock"
                style="padding-bottom:0.6rem;"
              >
                {{ password }}
              </v-text-field>

              <v-btn
                @click="onSignIn"
                height="4.3rem"
                type="button"
                block
                elevation="4"
                x-large
                class="btn"
                color="#5f48ea !important"
                justify-center
                align-center
                align-text
              >
                Login
              </v-btn>
            </v-form>
          </v-container>
        </v-card>
      </v-container>
    </v-main>
    <!-- footer -->
    <v-footer app> </v-footer>
  </v-app>
</template>

<script>
import { mapActions } from "vuex";
import ActionsTypes from "../store/types/actions-types";

export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    ...mapActions({
      LoginUser: ActionsTypes.POST_USER_DATA_ACTION,
    }),
    onSignIn() {
      console.log("Signing in .....");
      this.LoginUser({
        email: this.email,
        password: this.password,
      })
        .then((res) => {
          console.log("Login succeeded");
          this.$router.push("/home");
          console.log(res);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
.container {
  width: 38%;
  height: auto;
}

.cardContainer {
  width: 88%;
}

.btn {
  color: #fff !important;
  text-transform: lowercase;
  font-size: 1.2rem;
  font-weight: 800;
  text-transform: capitalize;
}

.tilte {
  color: black;
  font-size: 3rem;
  font-weight: 700;
}

.label {
  font-weight: 500;
  font-size: 1rem;
  line-height: 11px;
  color: #292d34;
  padding: 0 0 0.5rem 0.125rem;
}

.field {
  margin: 0 0 0.469rem;
}

.right-text {
  display: flex;
  font-size: 1.5rem;
  justify-items: center;
  font-weight: 400;
  color: #292d34;
}

.right-btn {
  width: 8rem;
  font-size: 1.213rem;
  text-transform: capitalize;
  margin-right: 1rem;
  color: #5f48ea !important;
  font-weight: 800;
  box-shadow: 0 5px 15px rgb(0 0 0 / 15%);
}
</style>

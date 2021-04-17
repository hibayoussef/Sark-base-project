<template>
  <v-app>
    
    <v-card  min-width="40rem" color="white" flat height="9rem">
      <v-toolbar min-width="44rem" flat height="133">
        <v-toolbar-items>
          <v-img class="logo" src="../../../../src/assets/logo_base.png" />
        </v-toolbar-items>

        <v-spacer></v-spacer>

        <v-toolbar-title class="right-text pa-8">
          Already playing with Slark?
        </v-toolbar-title>

        <v-btn x-large color="#fff" class="right-btn">
          Login
        </v-btn>
      </v-toolbar>
    </v-card>
    <!-- resizing the content -->
    <v-main  min-width="40rem">
      <v-container class="container">
        <v-card
                   min-width="20rem"
          class="mx-auto mt-5 pa-5 text-center rounded-lg overflow-hidden"
          id="limited-products"
        >
          <div class="text-center tilte ma-9">Let's go!</div>

          <v-container class="cardContainer">
            <v-form>
              <div class="text-left label">
                Full Name
              </div>
              <v-text-field
                placeholder="Micheal Dawod"
                v-model="name"
                type="text"
                required
                persistent-hint
                outlined
                prepend-inner-icon="mdi-account"
                class="field"
              >
                {{ name }}
              </v-text-field>

              <div class="text-left label">
                Email
              </div>
              <v-text-field
                v-model="email"
                type="text"
                placeholder="example@site.com"
                required
                persistent-hint
                outlined
                prepend-inner-icon="drafts"
                class="field"
              >
                {{ email }}</v-text-field
              >

              <div class="text-left label">
                Choose Password
              </div>
              <v-text-field
                placeholder="password"
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
                @click="onSignUp"
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
                Play with Slark
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
      name: "",
      nameRules: [
        (v) => !!v || "Name is required",
        (v) => (v && v.length >= 5) || "Name must be bigger than 5 characters",
      ],
      email: "",
      emailRules: [
        (v) => !!v || "E-mail is required",
        (v) =>
          /^(([^<>()[\]\\.,;:\s@']+(\.[^<>()\\[\]\\.,;:\s@']+)*)|('.+'))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
            v
          ) || "E-mail must be valid",
      ],
      password: "",
      passwordRules: [
        (v) => !!v || "Password is required",
        (v) =>
          /(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{6,}/.test(v) ||
          "Password must contain at least lowercase letter, one number, a special character and one uppercase letter",
      ],
    };
  },
  
  methods: {
    ...mapActions({
      AddNewUser: ActionsTypes.GET_USER_DATA_ACTION,
    }),
    onSignUp() {
      const data = {
        name: this.name,
        email: this.email,
        password: this.password,
      };
      console.log(data);
      this.AddNewUser(data)
        .then((res) => {
          console.log("User is already exist rrrrrrrrrrrrr", res);
          this.$router.push("/confirm-email");
        })
        .catch((error) => {
          console.log(error);
        });
    },
  }
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

.logo {
  margin-left: 1.5rem;
  margin-bottom: 2.4rem;
  transform: scale(1.4);
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

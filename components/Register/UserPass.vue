<template>
  <div :key="2" v-else-if="state === 2">
    <v-form
      method="POST"
      @submit.prevent="goToNextPage"
      style="max-width: 600px; margin: auto"
      ref="form"
    >
      <v-row>
        <v-col cols="12" md="6">
          <v-text-field
            :rules="rules"
            solo
            flat
            hide-details="auto"
            :error-messages="error.username"
            :error="!!error.username"
            name="username"
            v-model="userData.username"
            placeholder="نام کاربری"
          >
            <template #label>
              نام کاربری <span style="color: red"><strong>* </strong></span>
            </template>
          </v-text-field>
        </v-col>
        <v-col cols="12" md="6">
          <v-text-field
            :rules="rules"
            solo
            flat
            hide-details="auto"
            type="email"
            :error-messages="error.email"
            :error="!!error.email"
            name="email"
            v-model="userData.email"
            placeholder="ایمیل"
          >
            <template #label>
              ایمیل <span style="color: red"><strong>* </strong></span>
            </template>
          </v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="6">
          <v-text-field
            :rules="rules"
            solo
            flat
            hide-details="auto"
            type="password"
            :error-messages="error.password"
            :error="!!error.password"
            :password="!passwordShow"
            v-model="userData.password"
            name="password"
            placeholder="رمز عبور"
          >
            <template #label>
              رمز عبور <span style="color: red"><strong>* </strong></span>
            </template>
          </v-text-field>
        </v-col>
        <v-col cols="12" md="6">
          <v-text-field
            type="password"
            :rules="rules"
            solo
            flat
            hide-details="auto"
            :error-messages="error.confirm_password"
            :error="!!error.confirm_password"
            :password="!passwordShow"
            v-model="userData.confirm_password"
            name="confirm_password"
            placeholder="تکرار رمز عبور"
          >
            <template #label>
              تکرار رمز عبور <span style="color: red"><strong>* </strong></span>
            </template>
          </v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="6">
          <v-text-field
            solo
            flat
            hide-details="auto"
            :error-messages="error.discount_code"
            :error="!!error.discount_code"
            v-model="userData.discount_code"
            name="discount_code"
            placeholder="کد تخفیف"
          />
        </v-col>
      </v-row>
      <div
        style="
          display: flex;
          flex-direction: row;
          justify-content: space-between;
          margin-top: 100px;
        "
      >
        <v-btn class="button-outline prev-btn" v-on:click="goToPrevPage()"
          >مرحله قبل</v-btn
        >

        <v-btn class="button-fill next-btn" v-on:click="goToNextPage()"
          >مرحله بعد</v-btn
        >
      </div>
    </v-form>
  </div>
</template>

<script>
export default {
  name: "user_pass",
  data() {
    return {
      userData: { ...this.$store.state.register.userData },
      passwordShow: false,
      rules: [(v) => !!v || "این مقدار لازم است"],
    };
  },
  computed: {
    error() {
      return this.$store.state.register.error;
    },
    state: {
      get() {
        return this.$store.state.register.state;
      },
      set(data) {
        return this.$store.commit("register/setState", data);
      },
    },
  },
  watch: {
    userData: {
      handler: function (val, oldVal) {
        this.$store.commit("register/setUserData", val);
      },
      deep: true,
    },
  },
  methods: {
    showPassword() {
      this.$data.passwordShow = !this.$data.passwordShow;
    },
    async goToNextPage(page) {
      if (!this.$refs.form.validate()) return;
      this.$nuxt.$loading.start();
      try {
        await this.$axios.post(
          "register_validate/",
          this.$store.state.register.userData
        );
        this.$store.commit("register/setError", {});
        this.state = this.state + 1;
      } catch (error) {
        let text = "";
        if (error.response !== undefined) {
          if (error.response.data.non_field_errors !== undefined) {
            error.response.data.non_field_errors.forEach((value) => {
              text += value;
            });
          }
          this.$notify({
            group: "foo",
            type: "error",

            title: "خطا در ثبت نام!!",
            text: text,
          });
          this.$store.commit("register/setError", error.response.data);
          if (
            Object.keys(error.response.data).some(
              (v) =>
                ![
                  "username",
                  "email",
                  "password",
                  "attend_code",
                  "discount_code",
                  "non_field_errors",
                ].includes(v)
            )
          )
            this.state = this.state - 1;
        }
      } finally {
        this.$nuxt.$loading.finish();
      }
    },
    async goToPrevPage(page) {
      this.$store.commit(
        "register/setState",
        this.$store.state.register.state - 1
      );
    },
  },
};
</script>

<style scoped lang="scss">
.prev-btn {
  transform: scale(1.2);
  transform-origin: right bottom;
  border-radius: 12px;
}

.next-btn {
  transform: scale(1.2);
  transform-origin: left bottom;
  border-radius: 12px;
}
</style>

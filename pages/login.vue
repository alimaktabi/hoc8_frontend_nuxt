<template>
  <div class="login">
    <div class="content">
      <h1>ورود به حساب کاربری</h1>
      <form @submit.prevent="logInUser(userData)" method="post">
        <form-text-input :error="error" name="username" v-model="userData.username" placeholder="نام کاربری"
                   icon="account"/>
        <form-text-input :error="error" :password="!passwordShow" v-model="userData.password" name="password"
                   placeholder="رمز عبور"
                   icon="key"/>
        <div>
          <div style="display: flex; justify-content: space-between; flex-wrap: wrap; padding: 10px">
            <div style="display: flex; justify-content: center; align-items: center; gap: 5px">
              <input type="checkbox" id="showPassword" v-model="passwordShow">
              <label for="showPassword">نمایش رمز عبور</label>
            </div>
            <NuxtLink to="password_reset/">رمز عبور خود را فراموش کرده اید؟</NuxtLink>
          </div>
          <input type="submit" value="ورود">
        </div>
      </form>
    </div>
    <div class="image">
      <img src="~/assets/images/login_image.svg">
    </div>
  </div>
</template>

<script>

export default {
  name: "login",
  head(){
    return{
      title: 'ورود'
    }
  },
  data() {
    return {
      passwordShow: false,
      userData: {username: '', password: ''},
      error: "",
      sending: false

    }
  },
  computed: {
    passwordType: function () {
      return (this.$data.passwordShow) ? 'text' : 'password';
    },
  },
  methods: {
    showPassword() {
      this.$data.passwordShow = !this.$data.passwordShow
    },
    async logInUser(userData) {
      if (this.$data.sending)
        return
      this.$nuxt.$loading.start()
      this.$data.sending = true
      try {
        let response = await this.$auth.loginWith('local', {
          data: userData,
        })

        this.$notify({
          group: 'foo',
          type: 'success',
          title: 'با موفقیت وارد شدید',
          text: 'الان به صفحه پروفایلتان منتقل می شوید'
        });
        this.$router.push('/account')
      } catch (error) {
        this.$notify({
          group: 'foo',
          type: 'error',

          title: 'نام کاربری یا رمز عبور اشتباه است',
          text: 'لطفا نام کاربری یا رمز عبورتان را اصلاح کنید'
        });
        this.$data.error = 'error'
        this.$data.sending = false
        this.$nuxt.$loading.finish()


      }
    },
  },
  mounted() {
    this.$store.commit('setFooterColor', '#C5E3E3')
  },
  auth: 'guest'
}
</script>

<style scoped lang="scss">
.login {
  background: #C5E3E3;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px;
  gap: 30px;

  .content, .image {
    width: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: auto;

  }

  @media screen and (max-width: 1000px) {
    .image {
      display: none;
    }
    .content{
      width: 100%;

    }
    .login{
      padding: 15px;
    }
  }


  h1 {
    font-style: normal;
    font-weight: 700;
    font-size: 32px;
    color: #004948;
  }

  input[type="submit"] {
    box-shadow: inset 0px -4px 4px rgba(255, 252, 252, 0.25);
    filter: drop-shadow(0px 8px 10px rgba(0, 146, 143, 0.25));
    background: linear-gradient(180deg, #03B9B5 0%, #009592 100%);
    border-radius: 15px;
    padding: 10px 15px;
    border: none;
    width: 100%;
    height: 70px;
    font-style: normal;
    font-weight: 700;
    font-size: 28px;
    color: #FEFEFE;
  }

  input[type="checkbox"] {
    background: none;
    border-radius: 5px;
    width: 15px;
    height: 15px;

    color: #FEFEFE;
  }
}

</style>

<template>
  <div class="container-fluid login">
    <div class="row">
        <LoginForm />
        <LoginRightHero />
    </div>
  </div>
</template>

<script>
import LoginForm from './LoginForm'
import LoginRightHero from './LoginRightHero'

export default {
  name: 'Login',
  components : {
    LoginForm,
    LoginRightHero
  },
  props: {
    msg: String
  }
}
</script>

<style scoped>

</style>

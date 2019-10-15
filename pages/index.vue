<template>
  <div class="container mt-5">
    <!-- /passes es considerado un booleano, la llave para hacer pasar o no -->
    <ValidationObserver ref="observer" v-slot="{ passes }">
      <b-form @submit.prevent="passes(onSubmit)">
        <ValidationProvider
          rules="required|email"
          name="email"
          v-slot="{ errors }"
        >
          <b-form-group label="Email address:">
            <b-form-input
              type="email"
              v-model="form.email"
              placeholder="Enter email"
            >
            </b-form-input>
            <small class="form-text text-danger">{{ errors[0] }}</small>
          </b-form-group>
        </ValidationProvider>

        <ValidationProvider
          rules="required"
          name="password"
          v-slot="{ errors }"
        >
          <b-form-group label="password">
            <b-form-input
              type="password"
              v-model="form.password"
              placeholder="Enter password"
            >
            </b-form-input>
            <small class="form-text text-danger">{{ errors[0] }}</small>
          </b-form-group>
        </ValidationProvider>

        <b-button type="submit" variant="primary" block>
          Submit
        </b-button>
      </b-form>
    </ValidationObserver>
  </div>
</template>

<script>
import axios from 'axios'
import { mapMutations } from 'vuex'
export default {
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      valor: false
    }
  },
  methods: {
    ...mapMutations(['login']),
    onSubmit() {
      const endPoint = 'https://newsletters.academlo.com/api/v1/auth/login'
      axios.post(endPoint, this.form).then((response) => {
        const user = response.data
        this.login(user)
        this.$router.push('/all')
      })

      alert('La sesión se inició correctamente')
    }
  }
}
</script>

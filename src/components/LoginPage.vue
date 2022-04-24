<template>
  <div class="text-xs-center">
    <v-container>
            <v-img
        :src="require('../assets/star.png')"
        class="my-3"
        contain
        height="200"
        width="600"
      />

      <div align="center">
        <v-row>
        <v-col cols="12" md="4">
          <div justify-center> <p class="font-weight-black">
     AWARD
    </p></div>
          <v-alert v-if="this.show" dense outlined type="error">
            Email Not Found
          </v-alert>
          <div>Enter Your Email Address</div>
          <div>
            <v-text-field
              label="Email"
              single-line
              v-model="email"
            ></v-text-field>
          </div>
          <div>
            <v-btn color="grey" v-on:click="login">Sign In</v-btn>
          </div></v-col>
        <v-col> </v-col>
      </v-row>
      </div>
    </v-container>
  </div>
</template>

<style scoped>
</style>

<script>
// import axios from 'axios'
export default {
  data () {
    return {
      email: '',
      show: false,
      result: ''
    }
  },
  methods: {
    async login () {
      const body = {
        email: this.email
      }
      await this.axios.post('http://localhost:3000/award/login', body, {
        headers: {
          'Access-Control-Allow-Origin': '*',
          'Content-type': 'application/json'
        }

      }).then((response) => {
        this.result = response
        this.$router.push({ name: 'card' })
      }).catch(() => {
        this.show = true
      })
      this.show = true
    }
  }
}
</script>

<template>
  <div>
    <div align="center">
          <v-icon v-if="this.show"  >No Awards Found</v-icon>
    </div>
    <div v-for="data in card" :key="data.id">
      <v-lazy
      v-model="isActive"
      :options="{
        threshold: 0.5,
      }"
      min-height="200"
      transition="fade-transition"
    >
        <v-card class="mx-auto" max-width="344" outlined color="transparent">
        <v-img
          height="150px"
          width=""
          :src="data.image">
        <v-list-item three-line>
            <v-list-item-content>
              <div justify="left"></div>
              <v-list-item-title class="text-right mb-1">
                <v-chip class="ma-2 toCapitalFirst" color="primary"> {{data.type}} </v-chip>
              </v-list-item-title>
            </v-list-item-content>

            <!-- <v-list-item-avatar
        tile
      ></v-list-item-avatar> -->
          </v-list-item>

          <v-card-actions> <v-chip color="white" >{{data.point}} Poin</v-chip> </v-card-actions>
        </v-img>
        <div class="font-weight-bold">{{data.name}}</div>
        </v-card>
    </v-lazy>
    </div>
    <v-pagination v-if="!this.show" v-model="page" :length="2"> </v-pagination>
  </div>
</template>

<script>

export default {
  data () {
    return {
      isActive: false,
      page: 1,
      card: {},
      show: false
    }
  },
  methods: {
    getList () {
      // console.log(Object.keys(this.$router.currentRoute.query).length)
      if (this.$router.currentRoute.query !== undefined && Object.keys(this.$router.currentRoute.query).length !== 0) {
        if (this.$router.currentRoute.query.type.length > 0 && this.$router.currentRoute.query.min && this.$router.currentRoute.query.max) {
          this.selected = this.$router.currentRoute.query.type
          const types = []
          for (let i = 0; i < this.$router.currentRoute.query.type.length; i++) {
            types.push('type=' + this.$router.currentRoute.query.type[i])
          }
          const params = types.join('&') + '&min=' + this.$router.currentRoute.query.min + '&max=' + this.$router.currentRoute.query.max
          this.axios.get('http://localhost:3000/award?' + params).then((response) => {
            if (response.data.length === 0) {
              console.log(this.show)
              this.show = true
            } else {
              this.card = response.data
              // this.empty = false
            }
          })
          console.log('if pertama')
          return console.log('ini params', params)
        } else if (this.$router.currentRoute.query.type.length > 0) {
          const types = []
          for (let i = 0; i < this.$router.currentRoute.query.type.length; i++) {
            types.push('type=' + this.$router.currentRoute.query.type[i])
          }
          const params = types.join('&')
          this.axios.get('http://localhost:3000/award/?', { params: params }).then((response) => {
            this.card = response.data
          })
        } else if (this.$router.currentRoute.query.min && this.$router.currentRoute.query.max) {
          const params = 'min=' + this.$router.currentRoute.query.min + '&max=' + this.$router.currentRoute.query.max
          this.axios.get('http://localhost:3000/award/?', { params: params }).then((response) => {
            this.card = response.data
          })
        }
        // this.axios.get('http://localhost:3000/award/')
      }
      this.axios.get('http://localhost:3000/award/').then((response) => {
        this.card = response.data
      })
    }
  },
  beforeMount () {
    this.getList()
  }
}
</script>

<style scoped>
.toCapitalFirst {
  text-transform: capitalize;
}
</style>

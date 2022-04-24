<template>
  <div>
    <v-card flat color="transparent">
    <v-card-actions>
         <span class="ma-2" align-right>Filter</span>
        <v-spacer></v-spacer>
        <v-btn icon to="/card">
          <v-icon
      class="ma-2"
      right-ali
    >
      mdi-close
    </v-icon>
        </v-btn>
      </v-card-actions>
      <!-- <v-subheader>Min and max default slider</v-subheader>
      <p>{{user}}</p> -->

      <v-card-text class="ma-2">
        <div>
          <v-chip v-if="chip2" class="ma-2" close @click:close="chip2 = false">
         Poin: {{ min }} - {{slider}}
        </v-chip>
        </div>
        <div>
          <v-chip v-if="chip1" class="ma-2" close @click:close="chip1 = false">
         Type: {{ selected.join(", ") }}
        </v-chip>
        </div>
        <div>
            <v-chip v-if="chip1 && chip2" class="ma-2" close @click:close="chip1 = false; chip2 = false; " to = '/card'>
         Clear Filter
        </v-chip>
        </div>
        <div>
          <v-row>
          <v-column
            ><v-text-field
              v-model="min"
              class="mt-0 pt-0"
              hide-details
              single-line
              type="number"
              style="width: 60px"
            ></v-text-field
          ></v-column>
          <v-spacer></v-spacer>
          <v-column>
            <v-text-field
              v-model="slider"
              class="mt-0 pt-0"
              hide-details
              single-line
              type="number"
              style="width: 60px"
            ></v-text-field>
          </v-column>
        </v-row>
        <v-row>
          <v-col class="pr-4">
            <v-slider
              v-model="slider"
              class="align-center"
              :max="max"
              :min="min"
              hide-details
              step="1000"
            >
              <template v-slot:append> </template>
            </v-slider>
          </v-col>
        </v-row>
        </div>
      </v-card-text>
    </v-card>
    <v-container>
      <v-checkbox label="All"></v-checkbox>
      <v-checkbox v-model="selected" label="Voucher" value="voucher"></v-checkbox>
      <v-checkbox v-model="selected" label="Products" value="products"></v-checkbox>
      <v-checkbox v-model="selected" label="Others"></v-checkbox>
    </v-container>
    <div align="center">
      <v-btn @click="getList"
      depressed
      color="primary"
    >
      Filter
    </v-btn>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    getList () {
      let params = {}
      if (this.chip2 === false) {
        params = {
          type: this.selected
        }
      } else if (this.chip1 === false) {
        params = {
          min: this.min,
          max: this.slider
        }
      } else {
        params = {
          min: this.min,
          max: this.slider,
          type: this.selected
        }
      }

      console.log(params)
      // this.axios.get('https://jsonplaceholder.typicode.com/todos/1', { params: params }).then((response) => {
      //   this.user = response
      this.$router.push({ name: 'card', query: params })
      // })
    }
  },
  data () {
    return {
      user: {},
      min: 10000,
      max: 500000,
      slider: null,
      selected: [],
      chip1: false,
      chip2: false,
      chip3: false,
      closeButton: true
    }
  },
  watch: {
    selected: function (val) {
      if (val.length > 0) {
        this.chip1 = true
      } else {
        this.chip1 = false
      }
    },
    slider: function () {
      if (this.slider > 10000) {
        this.chip2 = true
      } else {
        this.chip2 = false
      }
    }
  },
  // beforeMount () {
  //   this.getList()
  // },
  clearAll () {
    this.selected = []
    this.slider = null
    this.chip1 = false
    this.chip2 = false
    this.chip3 = false
  }
}
</script>

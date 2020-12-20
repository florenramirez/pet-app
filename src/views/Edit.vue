<template>
    <div>
         <nav class="navbar navbar-light bg-info">
            <a class="navbar-brand text-white" href="/">Pets</a>
         </nav>
          {{ item.name }}
              <!-- Edit Form-->
              <div class="home-view-container">
                <b-form @submit.prevent="editData">
                  <b-form-group id="name" label="Pet's Name:" label-for="exampleInput2">
                    <b-form-input
                      id="name"
                      type="text"
                      placeholder="Enter name"
                      v-model="items.name"
                      :value="items.name"
                    />
                  </b-form-group>

                  <b-form-group id="kind" label="Kind:" label-for="exampleInput3">
                    <b-form-select id="kind" :options="['cat', 'dog', 'hamster', 'bird', 'fish', 'turtle', 'rabbit']" v-model="posts.kind" />
                  </b-form-group>

                  <b-form-group id="breed" label="Pet's Breed:" label-for="exampleInput2">
                    <b-form-input
                      id="breed"
                      type="text"
                      v-model="posts.breed"
                      placeholder="Enter breed" />
                  </b-form-group>

                  <b-form-group id="age" label="Pet's Age:" label-for="exampleInput2">
                    <b-form-input
                      id="age"
                      type="number"
                      v-model="posts.age"
                      placeholder="Enter age" />
                  </b-form-group>

                  <b-form-group id="gender" label="Gender:" label-for="exampleInput3">
                    <b-form-select id="gender" :options="['male', 'female']" v-model="posts.gender" />
                  </b-form-group>

                  <b-form-group id="color" label="Pet's color:" label-for="exampleInput2">
                    <b-form-input
                      id="color"
                      type="text"
                      v-model="posts.color"
                      placeholder="Enter color" />
                  </b-form-group>

                  <b-button type="submit" variant="primary">Submit</b-button>
                </b-form>
              </div>
    </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import editLogo from '../assets/edit.png'
import deleteLogo from '../assets/delete.png'
import PetList from '../components/PetList'
import { mapState } from 'vuex'

Vue.use(VueAxios, axios)

export default {
  name: 'AddPet',
  data () {
    return {
      items: ['name', 'kind', 'breed', 'age', 'gender', 'color'],
      list: undefined,
      editLogo: editLogo,
      deleteLogo: deleteLogo,
      name: '',
      posts: {
        name: '',
        kind: '',
        breed: '',
        age: 0,
        gender: '',
        color: ''
      },
      components: {
        PetList
      }
    }
  },
  computed: {
    ...mapState(['item']),
    item () {
      return this.item.find(v => v.id === this.$route.params.id)
    }
  },
  methods: {
    getData () {
      axios.get('http://api-pets.fituapp.com/api/v1/pets?token=d38e99d9790733c939e88698afbc30b6')
        .then((res) => {
          this.list = res.data
        })
        .catch((e) => {
          console.warn(e)
        })
    },
    editData (id) {
      this.axios.put(`http://api-pets.fituapp.com/api/v1/pets/${id}/?token=d38e99d9790733c939e88698afbc30b6`, this.items)
        .then((res) => {
          this.items = res.data
          console.warn(this.items)
        })
      // console.warn(this.posts)
    }
  },
  mounted () {
    this.getData()
  }
}
</script>

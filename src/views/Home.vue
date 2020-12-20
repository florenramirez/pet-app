<template>
  <div>
    <nav class="navbar navbar-light bg-info">
      <a class="navbar-brand text-white" href="/">Pets</a>
    </nav>
    <div>
      <a href='/' class="text-decoration-none text-dark">
      <PetList />
      </a>
    </div>
    <!-- Add Pet -->
  <div class="home-view-container">
    <button @click="togglePetForm" class="btn btn-primary mb-5">Add New Pet</button>
    <b-form @submit.prevent="postData" v-if="showPetForm">
      <b-form-group id="exampleInputGroup2" label="Pet's Name:" label-for="exampleInput2">
        <b-form-input
          id="exampleInput2"
          type="text"
          v-model="posts.name"
          required
          placeholder="Enter name" />
      </b-form-group>

      <b-form-group id="exampleInputGroup3" label="Kind:" label-for="exampleInput3">
        <b-form-select id="exampleInput3" :options="['cat', 'dog', 'hamster', 'bird', 'fish', 'turtle', 'rabbit']" required v-model="posts.kind" />
      </b-form-group>

      <b-form-group id="exampleInputGroup2" label="Pet's Breed:" label-for="exampleInput2">
        <b-form-input
          id="exampleInput2"
          type="text"
          v-model="posts.breed"
          required
          placeholder="Enter breed" />
      </b-form-group>

      <b-form-group id="exampleInputGroup2" label="Pet's Age:" label-for="exampleInput2">
        <b-form-input
          id="exampleInput2"
          type="number"
          v-model="posts.age"
          required
          placeholder="Enter age" />
      </b-form-group>

      <b-form-group id="exampleInputGroup3" label="Gender:" label-for="exampleInput3">
        <b-form-select id="exampleInput3" :options="['male', 'female']" required v-model="posts.gender" />
      </b-form-group>

      <b-form-group id="exampleInputGroup2" label="Pet's color:" label-for="exampleInput2">
        <b-form-input
          id="exampleInput2"
          type="text"
          v-model="posts.color"
          required
          placeholder="Enter color" />
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import PetList from '../components/PetList'

Vue.use(VueAxios, axios)
// import { mapActions } from 'vuex'

export default {
  name: 'Home',
  components: {
    PetList
  },
  data () {
    return {
      showPetForm: false,
      posts: {
        name: null,
        kind: null,
        breed: null,
        age: null,
        gender: null,
        color: null
      }
    }
  },
  methods: {
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    postData () {
      this.axios.post('http://api-pets.fituapp.com/api/v1/pets?token=d38e99d9790733c939e88698afbc30b6', this.posts)
        .then((res) => {
          console.warn(res)
        })
      // console.warn(this.posts)

      // reset form after submit
      this.posts = {
        name: '',
        kind: '',
        breed: '',
        age: 0,
        gender: null,
        color: ''
      }
    }
  }
}
</script>

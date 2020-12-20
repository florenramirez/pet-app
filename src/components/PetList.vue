<template>
    <div>
        <table class="table table-striped">
          <thead class="light">
          <tr>
            <th scope="col" class="text-info">ID</th>
            <th scope="col" class="text-info">Name</th>
            <th scope="col" class="text-info">Kind</th>
            <th scope="col" class="text-info">Breed</th>
            <th scope="col" class="text-info">Age</th>
            <th scope="col" class="text-info">Gender</th>
            <th scope="col" class="text-info">Color</th>
            <th scope="col" class="text-info"></th>

          </tr>
          <tr v-for="item in list" v-bind:key="item.id" >
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.kind}}</td>
            <td>{{item.breed}}</td>
            <td>{{item.age}}</td>
            <td>{{item.gender}}</td>
            <td>{{item.color}}</td>
            <td>
              <div class="home-view-container">
                <router-link :to="'/pet/' + item.id ">
                  <img :src="editLogo" height="20" width="20" class="mt-0"/>
                </router-link>
              </div>

              <button v-on:click.prevent="deletePet(item.id)" class="btn btn-link">
                <img :src="deleteLogo" height="20" width="20" class="mt-0"/>
              </button>
            </td>
          </tr>
          </thead>
        </table>
    </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import editLogo from '../assets/edit.png'
import deleteLogo from '../assets/delete.png'

Vue.use(VueAxios, axios)

export default {
  name: 'PetList',
  data () {
    return {
      list: undefined,
      editLogo: editLogo,
      deleteLogo: deleteLogo,
      showEditForm: false,
      name: '',
      posts: {
        name: '',
        kind: '',
        breed: '',
        age: 0,
        gender: '',
        color: ''
      }
    }
  },
  methods: {
    toggleEditForm () {
      this.showEditForm = !this.showEditForm
    },
    getData () {
      axios.get('http://api-pets.fituapp.com/api/v1/pets?token=d38e99d9790733c939e88698afbc30b6')
        .then((res) => {
          this.list = res.data
        })
        .catch((e) => {
          console.warn(e)
        })
    },
    deletePet (id) {
      this.axios.delete(`http://api-pets.fituapp.com/api/v1/pets/${id}/?token=d38e99d9790733c939e88698afbc30b6`)
        .then(() => {
          this.getData()
        })
    }
  },
  mounted () {
    this.getData()
  }
}
</script>

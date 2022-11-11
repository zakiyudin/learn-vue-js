<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <HeaderComponent v-bind:TextHeader="text_header"/>
  <h5>Selamat datang: {{ name }}</h5>
  <input type="text" v-model="name"><br>
  <button v-on:click="ubahNama">Ubah Nama</button>

  <p>------------------------------------------------</p>
  <!-- filter search dari title -->
  <input type="text" v-model="search">
  <!-- end filter search -->

  <div v-if="products.length !== 0">
    <ul>
      <li v-for="list in filterSearch" v-bind:key=list.id>
        {{ list.title }} : {{ list.price }}
      </li>
    </ul>
  </div>
  <div v-else>
    <p>[empty]</p>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'

export default {
  name: 'App',
  components: {
    HeaderComponent
  },
  data() {
    return {
      search: '',
      name: '',
      products: [],
      text_header: "Selamat Datang Gaiss 💚"
    }
  },
  methods: {
    ubahNama() {
      this.name = 'Kok nama ku diubah si 😑'
    }
  },
  created() {
    this.products = [
        { id: 1, title: "Product 1", price: 5000 },
        { id: 2, title: "Product 2", price: 4500 },
        { id: 3, title: "Product 3", price: 3700 },
        { id: 4, title: "Product 4", price: 1200 },
    ]
  },
    // * using computed properties
  computed: {
    // * method untuk me-filter by title
    filterSearch() {
      return this.products.filter(product => {
        return product.title.match(this.search)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

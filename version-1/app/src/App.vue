<template>
  <div id='app'>
    <Header></Header>
    <main>
      <JobList id="job-list" :listings="listings"></JobList>
      <JobForm :addListing="addListing"></JobForm>
    </main>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'
import JobList from './components/JobList'
import JobForm from './components/JobForm'
export default {
  name: 'app',
  components: {
    Header,
    Footer,
    JobList,
    JobForm
  },
  data () {
    return {
      listings: [],
      apiURL: '../static/listings.json'
    }
  },
  mounted () {
    fetch(this.apiURL)
      .then(response => response.json())
      .then(data => {
        this.listings = data
      })
  },
  methods: {
    addListing (listing) {
      this.listings.splice(0, 0, listing)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  margin: 0 30px 0 30px;
  padding: 0;
  font-family: sans-serif;
  color: #1B997A;
  display: grid;
  grid-template-rows: 15% 75% 10%;
}
main {
  grid-row: 2/3;
  display: grid;
  grid-template-columns: 5% 42.5% 5% 42.5% 5%;
}
#job-list {
  grid-column: 2/3;
}
</style>
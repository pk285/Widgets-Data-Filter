<template>
  <div class="container-fluid">
    <div class="search-wrapper">
    <!-- the search bar form -->
      <form v-on:submit="getfilteredData">
        <div class="form-row">
          <div class="col-10">
            <h1>Page Title</h1>
            <hr>
            <input type="text" class="form-control" placeholder="Enter city name" v-model="search" v-on:keyup="getfilteredData">
          </div>
        </div>
      </form>
  </div>
  <!-- end of checkboxes -->
  <div class="card-columns">
    <!-- iterate data -->
    <item-card v-for="(item, index) in filteredData" :key="index" :item="item"></item-card>
   </div>
  </div>
</template>
<script>
import ItemCard from './ItemCard';
import data from '../data/data';
export default {
  name: 'SearchPage',
  components: {
    'item-card': ItemCard
  },
  computed: {
    selectedFilters: function() {
      let filters = [];
      let checkedFiters = this.phones.filter(obj => obj.checked);
      checkedFiters.forEach(element => {
        filters.push(element.value);
      });
      return filters;
    }
  },
  data() {
    return {
      filteredData: [],
      search: '',
      phones: [
      
      ]
    };
  },
  methods: {
    getfilteredData: function() {
      this.filteredData = data;
      let filteredDataByfilters = [];
      let filteredDataBySearch = [];
      // first check if filters where selected
      if (this.selectedFilters.length > 0) {
        filteredDataByfilters= this.filteredData.filter(obj => this.selectedFilters.every(val => obj.stack.indexOf(val) >= 0));
        this.filteredData = filteredDataByfilters;
      }
      // then filter according to keyword, for now this only affects the name attribute of each data
      if (this.search !== '') {
        filteredDataBySearch = this.filteredData.filter(obj => obj.name.indexOf(this.search.toLowerCase()) >= 0);
        this.filteredData = filteredDataBySearch;
      }
    }
  },
  mounted() {
    this.getfilteredData();
  }
};
</script>
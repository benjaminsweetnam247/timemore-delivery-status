<template>
  <input type="text" placeholder="Filter by country" v-model="filter">
  <span>   Sort By:  
  <button v-on:click="this.sortby='country'">Country</button>
  <button v-on:click="this.sortby='status'">Status</button>
  <button v-on:click="this.sortby='date'">Shipping Date</button>
  </span>
  <table>
    <thead>
      <tr>
        <th>Country</th>
        <th>Status</th>
        <th>Shipping Date</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in filteredRows">
        <td>{{ row.country }}</td>
        <td>{{ row.status }}</td>
        <td>{{ row.date }}</td>
      </tr>
    </tbody>
  </table>
  <p>* Shipping date contingent on timely reglatory approval</p>
</template>

<script>
  import json from '../assets/data.json'
  export default {
    data() {
      return {
        sortby: 'country',
        direction: 1,
        filter:'',
        rows: json.countries
      }
    },
    computed: {
      filteredRows() {
        return this.rows.filter(row => {
          const country = row.country.toString().toLowerCase();
          const status = row.status;
          const date = row.date;
          const searchTerm = this.filter.toLowerCase();
          return country.includes(searchTerm);
        }).sort((a,b) => {
          let fa, fb
          switch (this.sortby) {
            case "country":
              fa = a.country.toString().toLowerCase(), fb = b.country.toString().toLowerCase();
              break;
            case "status":
              fa = a.status.toString().toLowerCase(), fb = b.status.toString().toLowerCase();
              break;
            case "date":
              fa = a.date.toString().toLowerCase(), fb = b.date.toString().toLowerCase();
              break
            default:
              fa = a.country.toString().toLowerCase(), fb = b.country.toString().toLowerCase();
          }
          if (fa < fb) {
            return -this.direction
          }
          if (fa > fb) {
            return this.direction
          }
          return 0
        });
      }
    }
  }
</script>

<style>
  table {
    width: 1000px;
  }
  tr {
    width: 100%;
  }
  td {
    width: 33%;
    border-bottom: 1px solid black
  }
  input {
    margin-bottom: 5rem;
  }
</style>
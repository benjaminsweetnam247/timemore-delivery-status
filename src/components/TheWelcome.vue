<template>
  <input type="text" placeholder="Filter by country" v-model="filter">
  <table>
    <thead>
      <tr>
        <th>Country</th>
        <th>Status</th>
        <th>Delivery Date</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in filteredRows" :key="row.country">
        <td>{{ row.country }}</td>
        <td>{{ row.status }}</td>
        <td>{{ row.date }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
  import json from '../assets/data.json'
  export default {
    data() {
      return {
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
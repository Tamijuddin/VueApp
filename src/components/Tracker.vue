<template>
<div> 
    <ul>
        <li>Total Cases in India: {{ summary.total}} </li>
        <li>Confirmed Cases Indian: {{ summary.confirmedCasesIndian}} </li>
        <li>Confirmed Cases Foreign: {{ summary.confirmedCasesForeign}} </li>
        <li>Discharged: {{ summary.discharged}} </li>
        <li>Deaths: {{ summary.deaths}} </li>
        <li>Confirmed But Location Unidentified: {{ summary.confirmedButLocationUnidentified}} </li>
        <li>Last Refreshed: {{ changeDate(refresh) }}</li>
</ul>
    <b-container fluid="sm">
<table class="table">
      <thead>
          <tr class="tr">
          <th scope="col">Location </th>
          <th scope="col">Confirmed Cases</th>
          <th scope="col">Discharged</th>
          <th scope="col">Foreign Cases </th>
          <th scope="col">Deaths</th>
            
        </tr>
        </thead>
      <tbody>
        <tr v-for="region in sortArray(regional)" v-bind:key="region.loc"> 
          <th scope="row">{{region.loc}}</th>
          <td>{{region.confirmedCasesIndian}}</td>
          <td>{{region.discharged}}</td>
          <td>{{region.confirmedCasesForeign}}</td>
          <td>{{region.deaths}}</td>
        </tr>
      </tbody>
    </table> 
    </b-container>
    <hr>
</div>      
</template>

<script>

import axios from 'axios';

export default {
    data(){
    return {
    regional:[],
    summary:{},
    refresh:''
    }
  },
  methods:{
    changeDate(date){
      var x = new Date(date);
      return x.toUTCString()
    },
    sortArray(x){
      var arr = [];
      arr=x.sort(function(a, b){return b.confirmedCasesIndian - a.confirmedCasesIndian});
      return arr;
    }
  },
mounted(){
    axios.get('https://api.rootnet.in/covid19-in/stats/latest')
    .then(response => {
      console.log(response);
      this.regional = response.data.data.regional,
      this.summary = response.data.data.summary,
      this.refresh = response.data.lastRefreshed
    })
  }
}
</script> 

<style scoped>
    table {
      position: relative;
        width: 100%;
        align-self: center;
        font-family: 'archia';
        text-transform: none;
        border-spacing: 3px 2px;
        border-collapse: separate;
    }
    ul{
      position: relative;
        width: 100%;
        text-align: left;
        font-family: 'archia';
    }
    thead {
          background: purple-light;
          color: gray-dark;
          text-align: center;
          font-size: 0.9rem;
    }
    th {
            padding: 0.5rem;
            cursor: pointer;
            border-radius: 5px;
            transition: all 0.1s ease-in-out;
            z-index: 99;
    }
    td {
            padding: 0.25rem;
            font-size: 0.7rem;
            border-radius: 5px;
            text-align: left;
    }
</style>

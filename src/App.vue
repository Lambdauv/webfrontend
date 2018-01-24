<template>
    <div id="app">
        <h1>ICDataServer</h1>
        <p>Data set #:
            <input v-model="start"/>
            <input v-model="stop"/>
            <button v-on:click="query">Query</button>
        </p>
        <vue-good-table
            title=""
            :columns="columns"
            :rows="rows"
            :paginate="true"
            :lineNumbers="false"/>
    </div>
</template>

<script>
import _ from 'lodash';
const rownames = ['job_id', 'cryostat', 'username', 'device', 'nmeas', 'jobsubmit',
    'jobstart', 'jobstop', 'jobstatus', 'dataserver', 'download'];

export default {
  name: 'App',

  data(){ return {
      start: '',
      stop: '',
      columns: [
          {
              field: "job_id",
              label: "Job ID"
          },
          {
              field: "cryostat",
              label: "Cryostat"
          },
          {
              field: "username",
              label: "Username"
          },
          {
              field: "device",
              label: "Device"
          },
          {
              field: "nmeas",
              label: "Cooldown #"
          },
          {
              field: "jobsubmit",
              label: "Job submit"
          },
          {
              field: "jobstart",
              label: "Job start"
          },
          {
              field: "jobstop",
              label: "Job stop"
          },
          {
              field: "jobstatus",
              label: "Job status"
          },
          {
              field: "dataserver",
              label: "Data server"
          },
          {
              field: "download",
              label: "Download",
              html: true
          }
       ],
       rows: []
    }
  },
  methods: {
      query: function () {
          var letterNumber = /^[0-9]+$/;

          this.$http.get('http://localhost:3000/listjobs/'+this.start+'/'+this.stop).then(response=>{
                  var d = response.data
                  var d2 = []
                  _.forEach(d, function(value) {
                      var r = _.mapValues(value, String)
                      r['download'] = '<a href="http://localhost:3000/download/'+value.job_id+'">Download</a>'
                      d2.push(r)
                  });
                  console.log(d2)
                  this.rows = d2
              }, response=>{
                  console.log('badness')
              }
          )
      }
    },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

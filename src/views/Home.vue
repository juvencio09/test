<template>
  <v-container>
    <v-row class="mt-8">
      <v-col cols="10">
        <h1>Reportes de ventas</h1>
      </v-col>
      <v-col cols="2">
        <v-btn @click="seeNew">Nuevo reporte</v-btn>
      </v-col>
    </v-row>
    <v-row>
      <tabla :report="reports"/>
    </v-row>
    <new :flagSee="falgSeeNew" @close="closeNew" @add="addNew"/>
  </v-container>
</template>

<script>
  import TablaReportes from '../components/TablaReportes'
  import NewReport from '../components/NewReport'

  export default {
    name: 'Home',
    components: { Tabla:TablaReportes, New:NewReport },
    data() {
      return {
        falgSeeNew: false,
        reports: []
      }
    },
    methods: {
      seeNew () {
        this.falgSeeNew = true;
      },
      closeNew () {
        this.falgSeeNew = false;
      },
      addNew (report) {
        this.reports.push(report)
        this.falgSeeNew = false;
      }
    }
  }
</script>

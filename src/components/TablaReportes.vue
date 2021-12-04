<template>
  <v-container>
      <v-data-table
        :headers="headers"
        :items="report"
        :items-per-page="5"
        class="elevation-1"
      >
        <template v-slot:[`item.actions`]="{}">
          <v-row>
            <v-col cols="6">
              <v-btn> borrar </v-btn>
            </v-col>
          </v-row>
        </template>
      </v-data-table>
  </v-container>
</template>

<script>
  export default {
    name: 'TablaReportes',
    props: ['report'],
    data: () => ({
      headers: [
          { text: 'Nombre del cliente' , value: 'name' },
          { text: 'Correo del cliente' , value: 'correo' },
          { text: 'Fecha'              , value: 'fecha' },
          { text: 'Total'              , value: 'total' },
          { text: 'Acciones'           , value: 'actions', width:200}
      ]
    })
  }
</script>

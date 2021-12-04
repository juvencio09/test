<template>
  <v-container>
      <v-dialog v-model="flagSee" persistent width="50%">
        <v-card style="padding:15px">
            <v-card-title>Nuevo reporte</v-card-title>

            <v-row style="padding: 30px 25px 0 25px">
                <v-col cols="12" style="margin:0px">
                        <v-text-field v-model="report.name" label="Nombre del cliente" solo></v-text-field>
                </v-col>
            </v-row>
            <v-row style="padding: 0 25px 0 25px">
                <v-col cols="12" style="padding-bottom:0px">
                        <v-text-field v-model="report.correo" label="Correo del cliente" solo></v-text-field>
                </v-col>
            </v-row>
            <v-row style="padding: 0 25px 0 25px">
                <v-col cols="6">
                    <v-menu
                        ref="menu"
                        v-model="menuIn"
                        :close-on-content-click="false"
                        transition="scale-transition"
                        offset-y
                        >
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                            v-model="report.fecha"
                            @click:append="menuIn = true"
                            append-icon="mdi-calendar"
                            label="Fecha"
                            solo
                            v-bind="attrs"
                            v-on="on"
                            >
                            </v-text-field>
                        </template>
                        <v-date-picker
                            ref="pickerBirth"
                            v-model="report.fecha"
                            min="1930-01-01"
                            @input="menuIn = false"
                        ></v-date-picker>
                        </v-menu>
                </v-col>
                <v-col cols="6" align="center">
                    <v-btn @click="falgSeeAdd = !falgSeeAdd">
                        AGREGAR PRODUCTO
                    </v-btn>
                </v-col>
            </v-row>
            <v-row justify="center" style="padding: 0 25px 20px 25px">
                <v-data-table
                    :headers="headers"
                    :items="product"
                    :items-per-page="3"
                    class="elevation-1"
                >
                        <template v-slot:[`item.actions`]="{}">
                        <v-row align="center">
                            <v-btn> borrar </v-btn>
                        </v-row>
                        </template>
                    </v-data-table>
            </v-row>

            <v-card-actions>
                <v-row>
                    <v-col cols="8">
                        <v-btn style="margin-right: 15px" @click='cancelarNew'>
                            Cancelar
                        </v-btn>
                        <v-btn :disabled='verificar()' @click='addReport'>
                            Guardar
                        </v-btn>
                    </v-col>
                    <v-col cols="4">
                        total: {{ total }}
                    </v-col>
                </v-row>

            </v-card-actions>
        </v-card>
    </v-dialog>
    <add :falg="falgSeeAdd" @close="closeAdd" @add="addItem"/>
  </v-container>
</template>

<script>
import NewItem from './NewItem'

export default {
    name: 'NewReport',
    props: ['flagSee'],
    components: { Add:NewItem },
    data: () => ({
        falgSeeAdd: false,
        total: 0,
        headers: [
          { text: 'Descripción'  , value: 'des' },
          { text: 'Departamento' , value: 'department' },
          { text: 'Precio'       , value: 'precio' },
          { text: 'Acciones'     , value: 'actions', width:100}
        ],
        product: [],
        report: { name:'' , fecha:'', correo:'', products: [], total:0},
        menuIn: false
    }),
    watch: {
      product: function (val) {
        if (val.length > 0) {
            this.total = 0
            this.report.total = 0
            for (let i = 0; i < val.length; i++) {
               this.total += parseInt(val[i].precio)
               this.report.total += parseInt(val[i].precio)
            }
        }
      }
    },
    methods: {
      cancelarNew () {
          this.$emit('close')
          this.report = { name:'' , fecha:'', correo:'', products: [], total:0}
          this.product = []
      },
      closeAdd() {
          this.falgSeeAdd = false
      },
      addReport() {
          this.report.product = this.product
          this.$emit('add', this.report)
          this.product = []
          this.report = { name:'' , fecha:'', correo:'', products: [], total:0}
      },
      addItem(item){
        this.product.push(item)
        this.falgSeeAdd = false
      },
      verificar () {
            if ( this.report.name === '' ||  this.report.fecha === '' ||  this.report.correo === '' || this.product.length === 0 ) {
                return true
            }
            return false
        }
      
    }
}
</script>

<style>

</style>
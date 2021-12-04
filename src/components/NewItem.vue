<template>
  <v-dialog width="40%" v-model="falg" persistent>
      <v-card style="padding: 15px">
          <v-card-title>Agregar producto</v-card-title>

            <v-row style="padding: 10px 15px 0 15px">
                <v-col cols="12" style="margin:0px">
                        <v-text-field v-model="product.des" label="Descripción" solo></v-text-field>
                </v-col>
            </v-row>
            <v-row style="padding: 0 15px 0 15px">
                <v-col cols="6" style="margin:0px">
                        <v-text-field v-model="product.department" label="Departamento" solo></v-text-field>
                </v-col>
                <v-col cols="6" style="margin:0px">
                        <v-text-field v-model="product.precio" label="Precio" type="number" solo></v-text-field>
                </v-col>
            </v-row>

            <v-card-actions>
                <v-btn @click='cancelarAdd'>
                    Cancelar
                </v-btn>
                <v-btn :disabled="verificar()" @click='addItem'>
                    Guardar
                </v-btn>
            </v-card-actions>
      </v-card>
  </v-dialog>
</template>

<script>
export default {
    props: ['falg'],
    data() {
        return {
            product: { des:'', department:'', precio:0}
        }
    },
    methods: {
        cancelarAdd () {
            this.$emit('close')
            this.product = { des:'', department:'', precio:0}
        },
        addItem () {
            this.$emit('add', this.product)
            this.product = { des:'', department:'', precio:0}
        },
        verificar () {
            if ( this.product.des === '' ||  this.product.department === '' ||  this.product.precio === '') {
                return true
            }
            return false
        }
    }
}
</script>

<style>

</style>
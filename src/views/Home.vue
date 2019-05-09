<template>
  <div>
    <!--
      wrap es usado como true,
      esto para que se respeten las 12 columnas
    -->
     <v-layout :wrap="true">
      <!--
        xs12: al configurar el punto de
        quiebre mas pequeñor, automaticamente
        este se hereda a los mas grandes, osea
        se usaran 12 columnas para xs, sm, md, lg y xl
      -->
      <v-flex xs12>
        <v-card>
          <v-date-picker
          v-model="fecha"
          full-width
          locale="es-cl"
          :min="minimo"
          :max="maximo"
          @change="getDolar(fecha)"
          >
          </v-date-picker>
        </v-card>
        <v-card color="error" dark>
          <v-card-text class="display-1 text-xs-center">
            <!--  Valor del dolar -->
            {{valor}}
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  data () {
    return {
      fecha: new Date().toISOString().substring(0, 10), // Fecha seleccionada por el usuario
      minimo: '1984', // valor minimo mostrado en el calendario
      maximo: new Date().toISOString().substring(0, 10), // valor maximo mostrado en el calendario (el dia actual)
      valor: null // Almacena el valor del dolar para mostrarlo bajo el calendario
    }
  },
  methods: {
    // Evento Asincrono que obtiene el valor del dolas desde un API
    async getDolar (dia) {
      let arrayFecha = dia.split('-')
      let ddmmyy = arrayFecha[2] + '-' + arrayFecha[1] + '-' + arrayFecha[0]
      try {
        let datos = await axios.get(`https://mindicador.cl/api/dolar/${ddmmyy}`)
        // Valido que contenga datos, en caso de dia sabado, domingo o festivo que no entrega el valor del dolas
        if (datos.data.serie.length > 0) {
          this.valor = await datos.data.serie[0].valor
        } else {
          this.valor = 'Sin resultados'
        }
      } catch (error) {
        console.log(error)
      }
    }
  },
  created () {
    this.getDolar(this.fecha)
  }
}
</script>

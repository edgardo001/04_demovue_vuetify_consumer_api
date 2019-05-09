<template>
  <!--Esta etiqueta es importante para usar coon vuetify-->
  <v-app>
    <!--
      v-container = Para centrar -> container de bootstrap
      v-layout = cada fila -> row de bootstrap
      v-flex = cada columnas -> col de bootstrap
    -->
    <v-content>
      <v-container>
        <router-view/>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      //
    }
  }
}
</script>

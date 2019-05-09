<template>
  <div>
    <!--
      wrap es usado como true,
      esto para que se respeten las 12 columnas
    -->
     <v-layout :wrap="true">
      <v-flex xs6 md6>
        <h1>Hola mundo!</h1>
      </v-flex>
      <v-flex xs2 md3>
        <h1>Hola mundo!</h1>
      </v-flex>
      <v-flex xs4 md3>
        <h1>Hola mundo!</h1>
      </v-flex>
      <v-flex xs4 md3>
        <h1>Hola mundo!</h1>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
export default {
  components: {
  }
}
</script>
